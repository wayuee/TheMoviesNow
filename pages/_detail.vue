<template>
<div>
  <div>
    <ul class="border-b-2 px-12 py-4 bg-indigo-200">
    <nuxt-link to="/" class="text-xl  ml-8 mb-20 font-bold pb-10"
      >The Movie Now</nuxt-link
    >
    </ul>
    <div class="mt-5 mr-96">
    <img :src="`http://image.tmdb.org/t/p/w500${detail.poster_path}`" class=" border rounded-xl float-left  mr-10 ml-44" style="height:530px;"/>
    <div class="text-4xl font-bold mb-5"> {{ detail.title }}</div>
    <h1>Release Date : <span class="font-bold">{{ detail.release_date }}</span></h1>
    <h1 class="inline-block">Genre : <span v-for="(data,id) in detail.genres" :key="id" class="font-bold">{{`${data.name}, `}}</span></h1>
    <h1>Run Time : <span class="font-bold">{{ detail.runtime }}m</span></h1>
    <h1 class=" mt-8 text-justify pb-5">{{ detail.overview }}</h1>
    <hr>
    <h1 class="pt-3">Production Studio:</h1>
    <span class="font-bold" v-for="(data,id) in detail.production_companies " :key="id">{{`${data.name},`}}</span>-
    <h1 class="pt-3">Stars: </h1>
    <span class="font-bold mb-10" v-for="(item,id) in stars" :key="id">{{`${item.original_name}, `}}</span>-
    <hr>
    </div>
  </div>
</div>
</template>

<script>

import axios from "axios"
export default {
  componentes:{
    axios,
  },
  data() {
    return {
      detail:{},
      stars:[],
      movieId:"",
    };
  },
  mounted() {
    this.getParam();
    this.getDataFromDetail();
    this.getCreditsApi();
  },
  methods: {
    getParam() {
      console.log(this.$route.query);
      console.log(this.$route.params);
      this.movieId = this.$route.query.id;
    },
    getDataFromDetail() {
    var api1 =`https://api.themoviedb.org/3/movie/${this.movieId}?api_key=6de3c0f0176c22fabe34c6be66fa8cae`
      axios
        .get(api1)
        .then((res) => {
          this.detail = res.data
          console.log(this.detail);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    getCreditsApi(){
      var api2 = `https://api.themoviedb.org/3/movie/${this.movieId}/credits?api_key=6de3c0f0176c22fabe34c6be66fa8cae`
      axios
        .get(api2)
        .then((res) => {
          this.stars = res.data.cast.slice(0, 10)
          console.log(this.stars);
        })
        .catch((err) => {
          console.log(err);
        });
    }
  },
};
</script>