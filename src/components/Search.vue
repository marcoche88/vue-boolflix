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
    <select class="form-select m-auto w-25">
      <option selected>Seleziona genere</option>
      <option :value="genre.name" v-for="genre in genres" :key="genre.id">
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