<template>
  <div id="app">
    <header>
      <div class="logo text-center text-uppercase p-2">
        <h1 class="text-red">Boolflix</h1>
      </div>
      <Search
        @search="search"
        placeholder="Inserisci un titolo di un Film o una Serie TV"
        :genres="genres"
        class="pb-3"
      />
    </header>
    <main class="pb-5">
      <Contents :results="movies" :genres="genres" title="Film" />
      <Contents :results="series" :genres="genres" title="Telefilm" />
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
      genres: [],
      key: "f7a805106989177ca0d6da798b3fd1eb",
      lang: "it-IT",
    };
  },
  methods: {
    search(query) {
      if (!query) {
        this.movies = [];
        this.series = [];
        return;
      }

      const params = {
        params: {
          api_key: this.key,
          language: this.lang,
          query,
        },
      };

      axios
        .get("https://api.themoviedb.org/3/search/movie", params)
        .then((res) => {
          this.movies = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
      axios
        .get("https://api.themoviedb.org/3/search/tv", params)
        .then((res) => {
          this.series = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
  created() {
    const params = {
      params: {
        api_key: this.key,
        language: this.lang,
      },
    };
    axios
      .get("https://api.themoviedb.org/3//genre/movie/list", params)
      .then((res) => {
        this.genres = res.data.genres;
      })
      .catch((err) => {
        console.log(err);
      });
  },
};
</script>

<style lang="scss">
@import "./scss/style.scss";
</style>
