<template>
<div>
  <div class="mt-10 ml-10" v-for="(data,id) in detail " :key="id">
    <nuxt-link to="/" class="text-xl px-12 py-4 bg-indigo-300 border rounded-xl ml-8 mb-20"
      >Back to Movie</nuxt-link
    >
    <div class="mt-10 mr-96">
    <img :src="`http://image.tmdb.org/t/p/w500${poster_path}`" class=" w-96 h-full border rounded-xl float-left  mr-10 ml-28" />
    <h1 class="text-4xl font-bold mb-5"> {{ param }}</h1>
    <h1 class="text-xl">Release Date : <span class="font-bold">{{  }}</span></h1>
    <h1 class="text-xl">Vote Everage : <span class="font-bold">{{  }}</span></h1>
    <h1 class="text-xl">Popularity : <span class="font-bold">{{ }}</span></h1>
    <h1 class="text-xl mt-10 text-justify pb-5">{{  }}</h1>
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
      movieId:"",
      param: "",
      poster_path:""
    };
  },
  mounted() {
    this.getParam();
    this.getDataFromDetail();
  },
  methods: {
    getParam() {
      console.log(this.$route.query);
      console.log(this.$route.params);
      this.param = this.$route.params.detail;
      this.movieId = this.$route.query.id
    },
    getDataFromDetail() {
    var api1 ="https://api.themoviedb.org/3/movie/634649?api_key=6de3c0f0176c22fabe34c6be66fa8cae"
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
  },
};
</script>