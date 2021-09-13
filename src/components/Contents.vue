<template>
  <section class="contents container">
    <h2 v-if="results.length" class="mt-5 text-red">{{ title }}</h2>
    <div class="row">
      <div
        class="col-xs-12 col-sm-6 col-md-4 col-lg-3 gy-5 h-400"
        v-for="result in results"
        :key="result.id"
      >
        <Card :cardItem="result" />
      </div>
    </div>
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
    results: Array,
    title: String,
  },
};
</script>

<style scoped lang="scss">
</style>