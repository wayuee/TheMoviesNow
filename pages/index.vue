<template>
  <div class="py-10">
    <div v-for="(data, id) in detailPage" :key="id"></div>
      <div class="flex flex-wrap justify-center">
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
      console.log(item.popularity);
      this.$router.push(
        `/${item.title}?id=${item.id}&poster_path=${this.poster_path}}`
      );
    },
  },
};
</script>

<style></style>
