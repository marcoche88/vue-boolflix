<template>
  <div class="card position-relative mx-3 h-100">
    <img
      class="poster card-img-top position-absolute h-100"
      v-if="cardItem.poster_path"
      :src="uriPoster + cardItem.poster_path"
      :alt="cardItem.title || cardItem.name"
    />
    <img
      class="poster card-img-top position-absolute h-100"
      v-else
      src="../assets/img/poster-placeholder.png"
      alt="no poster"
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
      uriPoster: "https://image.tmdb.org/t/p/w342",
    };
  },
  props: {
    cardItem: Object,
    genres: Array,
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