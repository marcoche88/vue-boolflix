<template>
  <section class="contents container">
    <div class="row">
      <div
        class="col-xs-12 col-sm-6 col-md-4 col-lg-3 gy-5 h-300 overflow-hidden"
        v-for="result in searchTot"
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
    searchTot: Array,
  },
};
</script>

<style scoped lang="scss">
.h-300 {
  height: 350px;
}
</style>