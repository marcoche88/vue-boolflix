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
            <strong>Lingua originale: </strong>
            <img
              v-if="flagImg(result.original_language)"
              :src="require(`../assets/img/${result.original_language}.png`)"
              :alt="result.original_language"
            />
            <span v-else>{{ result.original_language }}</span>
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
  methods: {
    flagImg(language) {
      return language === "it" || language === "en";
    },
  },
};
</script>

<style scoped lang="scss">
ol > li {
  margin: 10px 0;
}

img {
  width: 20px;
}
</style>