<template>
  <div id="app">
    <header>
      <div class="logo text-center text-uppercase p-2">
        <h1 class="text-red">Boolflix</h1>
      </div>
      <Search
        @search="search"
        placeholder="Inserisci un titolo di un Film o una Serie TV"
        :genres="allGenres"
        class="pb-3"
      />
    </header>
    <main class="pb-5">
      <Contents :results="movies" :genres="genresMovies" title="Film" />
      <Contents :results="series" :genres="genresSeries" title="Telefilm" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Search from "./components/Search.vue";
import Contents from "./components/Contents.vue";

export default {
  name: "App",
  components: {
    Search,
    Contents,
  },
  data() {
    return {
      movies: [],
      series: [],
      genresMovies: [],
      genresSeries: [],
      key: "f7a805106989177ca0d6da798b3fd1eb",
      lang: "it-IT",
      uriBase: "https://api.themoviedb.org/3",
    };
  },
  computed: {
    allGenres() {
      return [...this.genresMovies, ...this.genresSeries];
    },
  },
  methods: {
    search(query) {
      if (!query) {
        this.movies = [];
        this.series = [];
        return;
      }
      this.getFetch("/search/movie", "movies", query);
      this.getFetch("/search/tv", "series", query);
    },
    getFetch(endpoint, arr, query = "") {
      const params = {
        params: {
          api_key: this.key,
          language: this.lang,
          query,
        },
      };

      axios
        .get(`${this.uriBase}${endpoint}`, params)
        .then((res) => {
          console.log(res.data);
          if (endpoint.includes("genre")) {
            this[arr] = res.data.genres;
          } else {
            this[arr] = res.data.results;
          }
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  created() {
    this.getFetch("/genre/movie/list", "genresMovies");
    this.getFetch("/genre/tv/list", "genresSeries");
  },
};
</script>

<style lang="scss">
@import "./scss/style.scss";
</style>
