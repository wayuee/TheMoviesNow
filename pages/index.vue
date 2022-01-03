<template>
  <div class="pb-10">
    <ul class="bg-indigo-200 pt-3 pb-0.5">
    <h1 class="text-center font-bold text-xl mb-8 ">The Movie Now</h1>
    </ul>
    <div v-for="(data, id) in detailPage" :key="id"></div>
      <div class="grid grid-cols-4 gap-10 pt-5">
        <CardMovie
          v-for="(item, id) in results"
          :key="id"
          :data-movie="item"
          @click="toPageDetailMovie(item)"
        />
      </div>
  </div>
</template>

<script>
import axios from "axios";
import CardMovie from "~/components/mollecules/CardMovie";
export default {
  components: {
    axios,
    CardMovie,
  },
  data() {
    return {
      results: {},
      detailPage: [],
    };
  },
  mounted() {
    this.getDataFromMovie();
  },
  methods: {
    //GET= Ambil data , POST = Lempar data , PUT = edit data, DELETE = hapus data
    //Disingkat jadi CRUD = Create , Read , Update , Delete
    getDataFromMovie() {
      var api =
        "https://api.themoviedb.org/3/movie/now_playing?api_key=a4b5770b8ab225dfad78f779a8f3262c&language=en-US&page=1";
      axios
        .get(api)
        .then((res) => {
          this.results = res.data.results;
          console.log(this.results);
        })
        .catch((err) => {
          console.log(err);
        });
    },
    toPageDetailMovie(item) {
      this.$router.push(`/detail?id=${item.id}`
      );
    },
  },
};
</script>

<style></style>
