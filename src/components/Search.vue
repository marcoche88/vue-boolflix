<template>
  <div class="search-bar">
    <div class="input-group mb-3 w-50 m-auto">
      <input
        type="text"
        class="form-control"
        :placeholder="placeholder"
        v-model.trim="searchText"
        @keyup.enter="search"
      />
      <button class="btn btn-outline-danger" type="button" @click="search">
        Cerca
      </button>
    </div>
    <select
      v-model="genreInput"
      @change="filterGenre"
      class="form-select m-auto w-25"
    >
      <option value="all" selected>Tutti i generi</option>
      <option :value="genre.id" v-for="genre in genres" :key="genre.id">
        {{ genre.name }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      searchText: "",
      genreInput: "all",
    };
  },
  props: {
    placeholder: String,
    genres: Array,
  },
  methods: {
    search() {
      this.$emit("search", this.searchText);
      this.searchText = "";
    },
    filterGenre() {
      this.$emit("filterGenre", this.genreInput);
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";

input,
select {
  background-color: $secondary-bg-color;
  border-color: $border-color;
}
select {
  color: $primary-text-color;
}
</style>