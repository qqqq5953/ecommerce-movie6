<template>
  <Loading :active="isLoading"></Loading>
  <div class="bg-dark">
    <div class="container py-5">
      <div class="row justify-content-center mb-5">
        <div class="col-9">
          <PaginationForResults
            :totalPages="totalPages"
            :currentPage="currentPage"
            @change-page="setPagination"
            @previous-page="setPagination"
            @next-page="setPagination"
          ></PaginationForResults>
          <header>
            <div class="d-flex align-items-center">
              <!-- <i class="bi bi-film text-warning me-3 fs-4"></i> -->
              <i class="bi bi-play-btn-fill text-warning me-3 fs-2"></i>
              <!-- <i class="bi bi-play-circle-fill text-warning me-3 fs-3"></i> -->
              <!-- <i class="bi bi-badge-hd-fill text-warning me-3 fs-2"></i> -->
              <h2 class="h1 mb-0 text-white">Our Movies</h2>
            </div>
          </header>
          <ul class="mt-4 list-unstyled">
            <li class="mb-4" v-for="item in products" :key="item.id">
              <a
                href="#"
                class="text-decoration-none d-block"
                @click.prevent="getProductDetails(item.id)"
              >
                <!-- card -->
                <div class="movie-card">
                  <div class="info_section">
                    <div class="p-4" style="width: 60%">
                      <!-- card-header -->
                      <div class="row">
                        <div class="col-3">
                          <img
                            v-if="item.imageUrl[0]"
                            :src="item.imageUrl[0]"
                            class="card-img-top card-img-top-adjusted img-fluid d-block"
                            :alt="item.title"
                          />
                        </div>
                        <div class="col-9">
                          <h3 class="card-title mb-1">
                            {{ item.title }}
                          </h3>
                          <small class="d-inline-block me-2">{{
                            item.content.split('|')[2]
                          }}</small>
                          |
                          <small class="ms-2 d-inline-block"
                            >Popularity:
                            <span class="">{{
                              parseFloat(item.content.split('|')[1]).toFixed(0)
                            }}</span></small
                          >
                        </div>
                      </div>
                      <!-- card-body -->
                      <div class="row mt-3">
                        <div class="col-12">
                          <div class="card-text d-flex flex-column">
                            <p class="lh-sm">{{ item.description }}</p>

                            <div class="text-end mt-auto px-2">
                              <span> &#171; see more &#187;</span>
                            </div>
                          </div>
                        </div>
                      </div>
                    </div>
                  </div>
                  <div
                    class="backdrop_image"
                    :style="{ backgroundImage: `url(${item.imageUrl[1]})` }"
                  ></div>
                </div>
              </a>
            </li>
          </ul>
        </div>
      </div>
      <!-- <Pagination
        :pages="pagination"
        @change-page="getProducts"
        @previous-page="getProducts"
        @next-page="getProducts"
      ></Pagination> -->
    </div>
  </div>
</template>

<script>
// import Pagination from '@/components/Pagination.vue';
import PaginationForResults from '@/components/PaginationForResults.vue';

export default {
  components: {
    // Pagination,
    PaginationForResults
  },
  inject: ['emitter', 'sortData'],
  data() {
    return {
      allProducts: [],
      products: [],
      cart: [],
      status: {
        loadingItemsID: ''
      },
      isLoading: false,
      baseImageUrl: 'https://image.tmdb.org/t/p/w200',
      key: '7bbe6005cfda593dc21cceb93eaf9a8e',
      pagination: {},
      // pagination
      slicePages: undefined,
      totalPages: undefined,
      currentPage: 1,
      perPage: 3
      // genrePassIn: ''
    };
  },
  methods: {
    async getProducts(page = 1) {
      this.isLoading = true;

      // api
      const api = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/products?page=${page}`;
      const response = await this.$http.get(api).catch((err) => {
        console.log(err);
      });

      // 資料存入
      this.pagination = response.data.pagination;
      this.products = response.data.products;

      this.products.reverse();
      // this.products = this.sortData(this.products, 'content.split[1]');

      this.isLoading = false;
      console.log('res', response.data);
    },
    async getAllProducts() {
      // api
      const api = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/products/all`;
      const response = await this.$http.get(api).catch((err) => {
        console.log(err);
      });

      // 儲存資料並
      this.allProducts = response.data.products;

      // 排除訂閱的類型（重要）
      this.allProducts = this.allProducts.filter((item) => {
        return item.category !== 'Subscription';
      });

      // 照熱門度分類
      this.allProducts = this.sortData(this.allProducts, 'content');

      // 設置分頁
      this.setPagination();
    },
    setPagination(page = 1) {
      this.currentPage = page;

      // 設定總頁數、起訖頁
      this.totalPages = Math.ceil(this.allProducts.length / this.perPage);
      const startPage = this.currentPage * this.perPage - this.perPage;
      const endPage = startPage + this.perPage;

      this.products = this.allProducts.slice(startPage, endPage);
    },
    getProductDetails(id) {
      this.$router.push({ name: 'Product', params: { productID: id } });
    }
  },
  created() {
    window.scrollTo(0, -1000);

    this.getAllProducts();
  }
};
</script>

<style lang="scss" scoped>
.movie-card {
  position: relative;
  overflow: hidden;
  border-radius: 10px;
  box-shadow: 0px 0px 120px -20px rgba(0, 0, 0, 0.5);
  box-shadow: -6px 0px 50px -30px rgba(255, 255, 255, 0.8);

  &:hover {
    transform: scale(1.02);
    // box-shadow: 0px 0px 80px -25px rgba(0, 0, 0, 0.5);
    box-shadow: -6px 0px 55px -30px rgba(255, 255, 255, 1);
    transition: all 0.4s;
  }

  .info_section {
    background: linear-gradient(to right, #e5e6e6 50%, transparent 90%);
    background-blend-mode: multiply;
    position: relative;
    width: 100%;
    height: 100%;
    z-index: 2;

    .card-img-top-adjusted {
      object-fit: cover;
      object-position: center center;
      aspect-ratio: 2 / 3;
      max-height: 250px;
    }
  }

  .backdrop_image {
    background-repeat: no-repeat;
    background-size: cover;
    position: absolute;
    top: 0;
    right: 0;
    z-index: 1;
    height: 100%;
    width: 80%;
  }
}

.card-text {
  p {
    display: -webkit-box;
    // max-width: 90%;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }

  span:hover {
    color: #f0ad4e;
    font-weight: bold;
  }
}
</style>
