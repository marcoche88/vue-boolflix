<template>
  <div class="search-bar">
    <input type="text" v-model="searchText" />
    <button type="button" @click="search">Cerca</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Search",
  data() {
    return {
      searchText: "",
      searchRes: [],
      key: "f7a805106989177ca0d6da798b3fd1eb",
      lang: "it-IT",
    };
  },
  methods: {
    search() {
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${this.key}&query=${this.searchText}&language=${this.lang}`
        )
        .then((res) => {
          this.searchRes = res.data.results;
          this.$emit("search", this.searchRes);
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>

<style scoped lang="scss">
</style>