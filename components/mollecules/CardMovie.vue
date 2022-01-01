<template>
<div>
  <div class="px-10" >
    <button @click="addImage(dataMovie)">
    <img
      class="h-full w-72 "
      :src="`http://image.tmdb.org/t/p/w500${dataMovie.poster_path}`"
      alt="img not found"
    /></button>
    <div class="text-center pb-5 pt-2.5 font-semibold ">
    {{dataMovie.title}}
    </div>
  </div>
</div>
</template>

<script>
export default {
  props: {
    dataMovie: {
      type: Object,
      default: {},
    },
  },
  methods:{
    addImage(dataMovie){
      this.$emit("click",this.$router.push(`&poster_path=${dataMovie.poster_path}`))
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}
</style>
