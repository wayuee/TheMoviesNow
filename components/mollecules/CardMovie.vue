<template>
<div>
  <div class="xl:px-8 md:px-3 sm:ml-5 ">
    <button @click="addImage(dataMovie)">
    <img
      class="h-full w-60 border rounded-xl xl:w-80"
      :src="`http://image.tmdb.org/t/p/w500${dataMovie.poster_path}`"
      alt="img not found"
    /></button>
    <div class="text-center pb-5 pt-1 text-md md:text-lg lg:text-xl font-bold ">
    {{dataMovie.title}} ({{getDataYear(dataMovie.release_date)}})
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: {
    dataMovie: {
      type: Object,
      default: () => {},
    },
  },
  methods:{
    addImage(dataMovie){
      this.$emit("click",this.$router.push(`&poster_path=${dataMovie.poster_path}`))
    },
    getDataYear(){
      const date = new Date()
      const getYear = date.getFullYear()
      return getYear
    }
  },
}
</script>

<style>
  * {
    box-sizing: border-box;
  }
</style>
