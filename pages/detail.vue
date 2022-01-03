<template>
  <div>
    <div>
      <ul class="border-b-2 px-12 py-4 bg-indigo-200">
        <nuxt-link to="/" class="text-md ml-8 mb-20 font-bold pb-10 md:text-lg lg:text-xl xl:text-xl"
          >The Movie Now</nuxt-link
        >
      </ul>
      <div class="mt-5 mr-4 md:mr-10 lg:mr-20 xl:mr-40">
        <img
          :src="`http://image.tmdb.org/t/p/w500${detail.poster_path}`"
          class="border rounded-xl float-left mb-80 h-48 mr-4 sm:ml-2 md:ml-2 md:mb-40 lg:ml-20 xl:ml-40 "
          id="img"
        />
        <div class="text-lg md:text-xl lg:text-2xl xl:text-4xl font-bold mb-2 md:mb-5 lg:mb-6 xl:mb-8">{{ detail.title }}</div>
        <h1 class="text-xs md:text-sm lg:text-base xl:text-base">
          Release Date :
          <span class="font-bold">{{ detail.release_date }}</span>
        </h1>
        <h1 class="text-xs md:text-sm lg:text-base xl:text-base inline-block">
          Genre :
          <span
            v-for="(data, id) in detail.genres"
            :key="id"
            class="font-bold"
            >{{ `${data.name}, ` }}</span
          >
        </h1>
        <h1 class="text-xs md:text-sm lg:text-base xl:text-base">
          Run Time : <span class="font-bold">{{ detail.runtime }}m</span>
        </h1>
        <h1 class="text-xs md:text-sm lg:text-base xl:text-base mt-2 md:mt-5 lg:mt-6 xl:mt-8 text-justify pb-1 xl:pb-3 md:pb-3 lg:pb-3">{{ detail.overview }}</h1>
        <hr />
        <h1 class="text-xs md:text-sm lg:text-base xl:text-base pt-1 lg:pt-3 xl:pt-3 md:pt-3">Production Studio:</h1>
        <span
          class="text-xs md:text-sm lg:text-base xl:text-base font-bold"
          v-for="(data, id) in detail.production_companies"
          :key="id"
          >{{ `${data.name}, ` }}</span
        >-
        <h1 class="text-xs md:text-sm lg:text-base xl:text-base">Stars:</h1>
        <ul class="text-xs md:text-sm lg:text-base xl:text-base mb-2 md:mb-3 lg:mb-4 xl:mb-5">
          <span class="font-bold" v-for="(item, id) in stars" :key="id">{{
            `${item.original_name}, `
          }}</span
          >-
        </ul>
        <hr />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  componentes: {
    axios,
  },
  data() {
    return {
      detail: {},
      stars: [],
      movieId: "",
    };
  },
  mounted() {
    this.getParam();
    this.getDataFromDetail();
    this.getCreditsApi();
  },
  methods: {
    getParam() {
      this.movieId = this.$route.query.id;
    },
    getDataFromDetail() {
      var api1 = `https://api.themoviedb.org/3/movie/${this.movieId}?api_key=6de3c0f0176c22fabe34c6be66fa8cae`;
      axios
        .get(api1)
        .then((res) => {
          this.detail = res.data;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getCreditsApi() {
      var api2 = `https://api.themoviedb.org/3/movie/${this.movieId}/credits?api_key=6de3c0f0176c22fabe34c6be66fa8cae`;
      axios
        .get(api2)
        .then((res) => {
          this.stars = res.data.cast.slice(0, 10);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style>
@media (min-width: 768px) {
  #img{
    height: 400px;
  }
}

@media (min-width: 992px) {
  #img{
    height: 535px;
  }
}
</style>
