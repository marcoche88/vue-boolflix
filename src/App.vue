<template>
  <div id="app">
    <header>
      <div class="logo text-center text-uppercase p-2">
        <h1 class="text-red">Boolflix</h1>
      </div>
      <Search
        @search="search"
        @filterGenre="filterGenre"
        placeholder="Inserisci un titolo di un Film o una Serie TV"
        :genres="allGenres"
        class="pb-3"
      />
    </header>
    <main class="pb-5">
      <Contents :results="moviesFiltered" :genres="genresMovies" title="Film" />
      <Contents
        :results="seriesFiltered"
        :genres="genresSeries"
        title="Serie TV"
      />
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
      genreInput: "all",
      key: "f7a805106989177ca0d6da798b3fd1eb",
      lang: "it-IT",
      uriBase: "https://api.themoviedb.org/3",
    };
  },
  computed: {
    allGenres() {
      const arrGenres = [];
      this.genresSeries.forEach((genreTV) => {
        let isInclude = this.genresMovies.some((genreMovie) => {
          return genreMovie.id === genreTV.id;
        });
        if (!isInclude) arrGenres.push(genreTV);
      });
      return [...this.genresMovies, ...arrGenres];
    },
    moviesFiltered() {
      if (this.genreInput === "all") return this.movies;
      return this.movies.filter((movie) => {
        if (movie.genre_ids.includes(this.genreInput)) return true;
        return false;
      });
    },
    seriesFiltered() {
      if (this.genreInput === "all") return this.series;
      return this.series.filter((serie) => {
        if (serie.genre_ids.includes(this.genreInput)) return true;
        return false;
      });
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
    filterGenre(value) {
      this.genreInput = value;
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