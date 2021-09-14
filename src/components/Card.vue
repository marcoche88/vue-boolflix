<template>
  <div class="card position-relative mx-3 h-100">
    <img
      class="poster card-img-top position-absolute h-100"
      :src="imgPath"
      :alt="cardItem.title || cardItem.name"
    />
    <CardBody :cardItem="cardItem" :genres="genres" />
  </div>
</template>

<script>
import CardBody from "./CardBody.vue";

export default {
  name: "Card",
  components: {
    CardBody,
  },
  data() {
    return {
      urlPoster: "https://image.tmdb.org/t/p/w342",
    };
  },
  props: {
    cardItem: Object,
    genres: Array,
  },
  computed: {
    imgPath() {
      if (this.cardItem.poster_path) {
        return this.urlPoster + this.cardItem.poster_path;
      }
      return require("../assets/img/poster-placeholder.png");
    },
  },
};
</script>

<style scoped lang="scss">
.card {
  border: none;
  background-color: transparent;
}

.poster {
  z-index: -1;
}
</style>