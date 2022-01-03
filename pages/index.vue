<template>
  <div class="pb-10">
    <ul class="bg-indigo-200 pt-3 pb-0.5">
      <h1 class="text-center font-bold text-xl mb-8 ">The Movie Now</h1>
    </ul>
    <div class="grid grid-cols-2 gap-4 md:grid-cols-3 mr:gap-6 lg:grid-cols-4 lg:gap-6 xl:grid-cols-4 xl:gap-6 pt-5" id="min-width">
      <CardMovie
        v-for="(item, id) in results"
        :key="id"
        :data-movie="item"
        @click="toPageDetailMovie(item)"
      />
    </div>
    <Button @click="addMore" label-button="More"/>
  </div>
</template>

<script>
import axios from "axios";
import CardMovie from "~/components/mollecules/CardMovie";
import Button from "~/components/atoms/Button"
export default {
  components: {
    axios,
    CardMovie,
    Button,
  },
  data() {
    return {
      results: [],
      page: 1,
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
        `https://api.themoviedb.org/3/movie/now_playing?api_key=a4b5770b8ab225dfad78f779a8f3262c&language=en-US&page=${this.page}`;
      axios
        .get(api)
        .then((res) => {
          res.data.results.forEach(element => {
            this.results.push(element)
          });
        })
        .catch((err) => {
          console.log(err);
        });
    },
    toPageDetailMovie(item) {
      this.$router.push(`/detail?id=${item.id}`
      );
    },
    addMore(){
      this.page += 1
      this.getDataFromMovie()
    }
  },
};
</script>

<style></style>
