<template>
  <section class="contents">
    <ol>
      <li v-for="result in searchTot" :key="result.id">
        <ul>
          <li><strong>Titolo:</strong> {{ result.title || result.name }}</li>
          <li>
            <strong>Titolo originale:</strong>
            {{ result.original_title || result.original_name }}
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
  data() {
    return {
      flags: ["it", "en"],
    };
  },
  props: {
    searchTot: Array,
  },
  methods: {
    flagImg(language) {
      return this.flags.includes(language);
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