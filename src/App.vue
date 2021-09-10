<template>
  <div id="app">
    <header>
      <Search @search="searchResults" />
    </header>
    <main>
      <Contents :searchRes="searchRes" />
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
      searchRes: [],
    };
  },
  methods: {
    searchResults(arr) {
      this.searchRes = arr;
    },
  },
};
</script>

<style lang="scss">
</style>
