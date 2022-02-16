<template>
  <Loading :active="isLoading"></Loading>

  <!-- <header class="position-relative">
    <div
      class="header position-relative top-0 bottom-0 w-100"
      style="
        background: url('https://images.unsplash.com/photo-1478720568477-152d9b164e26?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&h=800&q=80');
      "
    ></div>
  </header> -->
  <!-- <header
    class="header"
    style="
      background: url('https://images.unsplash.com/photo-1626814026160-2237a95fc5a0?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1470&h=400&q=80');
      min-height: 400px;
    "
  ></header> -->
  <!-- <header
    class="header"
    style="
      background: url('https://images.unsplash.com/photo-1542204165-65bf26472b9b?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1374&h=300&q=80');
      min-height: 300px;
    "
  ></header> -->

  <div class="bg-primary">
    <header class="position-relative">
      <div
        class="header"
        style="
          background: url('https://images.unsplash.com/photo-1478720568477-152d9b164e26?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&h=800&q=80');
        "
      ></div>
      <div class="position-absolute top-0 bottom-0 w-100">
        <div
          class="d-flex align-items-center m-auto h-100"
          style="background: rgba(255, 255, 255, 0.2)"
        >
          <div class="" style="width: 43%">
            <div class="mb-0 ms-4 p-4" style="background: rgba(0, 0, 0, 0.45)">
              <h2 class="display-4 text-white">
                <span class="d-block">Offer</span>
                <span>worldwide</span>
                <span class="text-warning"> latest movies </span>
                fitting your lifestyle
              </h2>
              <hr class="my-0 text-white" />
              <div class="mt-3">
                <router-link
                  :to="{ name: 'AllProducts' }"
                  class="btn btn-warning fs-5 w-100"
                >
                  <span>Pick a movie now</span>
                  <i class="bi bi-arrow-right ms-2"></i>
                </router-link>
                <!-- <a href="#" type="button" class="btn btn-warning fs-5 w-100"> </a> -->
              </div>
            </div>
          </div>
        </div>
      </div>
    </header>
    <main class="container py-5">
      <!-- why CMDB -->
      <section class="">
        <h2 class="h1 text-white text-center mb-4">Why CMDB</h2>
        <ul class="row list-unstyled mb-0">
          <li class="col">
            <div class="rounded-3 p-4 h-100 why-section-background">
              <h3 class="text-white text-center">Flexibility</h3>
              <div class="d-flex justify-content-center my-3">
                <i class="bi bi-calendar-plus display-1 text-warning"></i>
              </div>
              <p class="text-white mb-4">
                <span>We offer 2 flexible plans:</span>
                <span class="d-block">
                  <span class="fw-bold text-warning">SUBSCRIPTION:</span>
                  unequaled entertainment experience</span
                >
                <span class="d-block">
                  <span class="fw-bold text-warning">RENTAL:</span>
                  prompt entertainment with high qualities.</span
                >
              </p>
              <p class="text-white">
                You can also subscribe for week
                <span class="fw-bold text-warning">only 1 month</span> or rent
                for
                <span class="fw-bold text-warning">only 1 week</span>
                if you like.
              </p>
            </div>
          </li>
          <li class="col">
            <div class="rounded-3 p-4 h-100 why-section-background">
              <h3 class="text-white text-center">Diversity</h3>
              <div class="d-flex justify-content-center my-3">
                <i class="bi bi-globe display-1 text-warning"></i>
              </div>
              <p class="text-white">
                We collect the latest movies from
                <span class="fw-bold text-warning"
                  >Asia, Europe, United States of America and Canada</span
                >
                , ensuring to keep on track of the trends.
              </p>
            </div>
          </li>
          <li class="col">
            <div class="rounded-3 p-4 h-100 why-section-background">
              <h3 class="text-white text-center">Quality</h3>
              <div class="d-flex justify-content-center gap-3 my-3">
                <i class="bi bi-badge-4k display-1 text-warning"></i>
                <i class="bi bi-badge-hd display-1 text-warning"></i>
              </div>
              <p class="text-white">
                We provide
                <span class="fw-bold text-warning">either 4K or HD</span>
                movies depending on the plan chosen, differentiating from the
                market where only premium members are qualified for the high
                quality entertainment.
              </p>
            </div>
          </li>
        </ul>
      </section>

      <!-- Playing Now -->
      <section class="pt-5">
        <h2 class="h1 d-inline-block">
          <a
            href="#"
            @click.prevent="moreResultsOfCMDB('nowplaying')"
            class="text-white text-decoration-none d-flex align-items-center"
          >
            <i class="bi bi-camera-reels text-warning me-3 fs-4"></i>
            <i
              class="bi bi-camera-reels-fill d-none text-warning me-3 fs-4"
            ></i>
            <span>Now Playing Movie</span>
            <i class="bi bi-chevron-right ms-2 fs-4"></i>
          </a>
        </h2>
        <div class="position-relative mt-3">
          <section class="overflow-auto card-scrollbar position-relative">
            <CardVertical
              :results="nowPlaying"
              :language="language"
            ></CardVertical>
          </section>
          <div class="position-absolute right-blur"></div>
        </div>
      </section>

      <!-- UpComing -->
      <section class="pt-5">
        <h2 class="h1 d-inline-block">
          <a
            href="#"
            @click.prevent="moreResultsOfCMDB('upcoming')"
            class="text-white text-decoration-none d-flex align-items-center"
          >
            <i class="bi bi-camera-reels text-warning me-3 fs-4"></i>
            <i
              class="bi bi-camera-reels-fill d-none text-warning me-3 fs-4"
            ></i>
            <span>UpComing Movie</span>
            <i class="bi bi-chevron-right ms-2 fs-4"></i>
          </a>
        </h2>
        <div class="position-relative mt-3">
          <section
            class="overflow-auto mt-3 mb-5 card-scrollbar position-relative"
          >
            <CardVertical
              :results="upComing"
              :language="language"
            ></CardVertical>
          </section>
          <div class="position-absolute right-blur"></div>
        </div>
      </section>
    </main>
  </div>
</template>

<script>
import CardVertical from '@/components/CardVerticalTest.vue';
// import Navbar from '@/components/Navbar.vue';

export default {
  components: {
    CardVertical
    // Navbar
  },
  inject: ['sortData', 'emitter'],
  data() {
    return {
      basrUrl: 'https://api.themoviedb.org/3/',
      key: '7bbe6005cfda593dc21cceb93eaf9a8e',
      products: [],
      nowPlaying: [],
      upComing: [],
      language: 'en-US',
      region: 'US',
      isLoading: false
    };
  },
  methods: {
    moreResultsOfCMDB(genre) {
      this.$router.push({ name: 'AllResults', params: { genre } });
    },
    async getProducts() {
      this.isLoading = true;

      // api
      const api = `${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/products/all`;
      const response = await this.$http.get(api).catch((err) => {
        console.log(err);
      });
      console.log('res', response.data);

      // 儲存資料
      this.products = response.data.products;

      // 將 nowPlaying 分離出來
      this.getNowPlaying();

      // 將 upComing 分離出來
      this.getUpcoming();

      this.isLoading = false;
    },
    getNowPlaying() {
      this.nowPlaying = this.products.filter((item) => {
        const genre = item.category.split('|')[1];
        return genre === 'nowplaying';
      });
    },
    getUpcoming() {
      this.upComing = this.products.filter((item) => {
        const genre = item.category.split('|')[1];
        return genre === 'upcoming';
      });
    }
  },
  created() {
    window.scrollTo(0, -1000);

    this.getProducts();
  }
};
</script>

<style lang="scss" scoped>
.header {
  background-repeat: no-repeat !important;
  background-position: 0% 60% !important;
  background-size: cover !important;
  height: 70vh;
  -moz-transform: scaleX(-1);
  -webkit-transform: scaleX(-1);
  -o-transform: scaleX(-1);
  transform: scaleX(-1);
}

.why-section-background {
  background: rgba(52, 58, 64, 0.3);
  border-radius: 16px;
  box-shadow: 0 0 8px rgba(255, 255, 255, 0.6);
  backdrop-filter: blur(13.5px);
  -webkit-backdrop-filter: blur(13.5px);
}

h2:hover {
  .bi-chevron-right {
    color: #f0ad4e;
  }

  .bi-camera-reels {
    display: none;
  }

  .bi-camera-reels-fill {
    display: block !important;
  }
}

.right-blur {
  width: 2.5rem;
  height: 435px;
  top: 0;
  right: 0;
  z-index: 10;
  background: linear-gradient(
    to left,
    rgba(24, 24, 24, 0.9) 15%,
    transparent 100%
  );
  // background: linear-gradient(to left, red 5%, transparent 100%);
}

.card-scrollbar {
  scroll-snap-type: x mandatory;
  overscroll-behavior-inline: contain;

  &::-webkit-scrollbar {
    height: 10px;
  }

  &::-webkit-scrollbar-track {
    // background-color: rgba(85, 89, 92, 1);
    background-color: rgba(69, 67, 56, 0.7);
    border-radius: 100vw;
    margin-inline: 10vw;
  }

  &::-webkit-scrollbar-thumb {
    background-color: rgba(255, 255, 255, 0.75);

    border-radius: 100vw;
    border: 2px solid rgba(85, 89, 92, 1);

    &:hover {
      background-color: rgba(26, 26, 26, 1);

      // background-color: #f0ad4e;
      border: 2px solid rgba(255, 255, 255, 0.7);
      border: 2px solid #f0ad4e;
    }
  }
}
</style>
