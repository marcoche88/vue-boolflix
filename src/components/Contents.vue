<template>
  <section class="contents">
    <ol>
      <Card v-for="result in searchTot" :key="result.id" :cardItem="result" />
    </ol>
  </section>
</template>

<script>
import Card from "./Card.vue";

export default {
  name: "Contents",
  components: {
    Card,
  },
  props: {
    searchTot: Array,
  },
};
</script>

<style scoped lang="scss">
</style>