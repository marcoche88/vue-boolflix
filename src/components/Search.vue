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
input {
  background-color: #202020;
  border-color: rgb(144, 144, 144);
}
</style>