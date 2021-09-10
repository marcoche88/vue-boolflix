<template>
  <div id="app">
    <header>
      <Search @searchMovies="searchResultsMovies" @searchTV="searchResultsTV" />
    </header>
    <main>
      <Contents :searchTot="searchTot" />
    </main>
  </div>
</template>

<script>
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
      searchResMovies: [],
      searchResTV: [],
    };
  },
  computed: {
    searchTot() {
      return [...this.searchResMovies, ...this.searchResTV];
    },
  },
  methods: {
    searchResultsMovies(arr) {
      this.searchResMovies = arr;
    },
    searchResultsTV(arr) {
      this.searchResTV = arr;
    },
  },
};
</script>

<style lang="scss">
</style>
