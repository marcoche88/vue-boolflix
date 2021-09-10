<template>
  <section class="contents">
    <ol>
      <li v-for="result in searchRes" :key="result.id">
        <ul>
          <li><strong>Titolo:</strong> {{ result.title }}</li>
          <li>
            <strong>Titolo originale:</strong> {{ result.original_title }}
          </li>
          <li>
            <strong>Lingua originale:</strong> {{ result.original_language }}
          </li>
          <li><strong>Voto:</strong> {{ result.vote_average }}</li>
        </ul>
      </li>
    </ol>
  </section>
</template>

<script>
export default {
  name: "Contents",
  props: {
    searchRes: Array,
  },
};
</script>

<style scoped lang="scss">
ol > li {
  margin: 10px 0;
}
</style>