<template>
  <li class="card">
    <ul>
      <li><strong>Titolo:</strong> {{ cardItem.title || cardItem.name }}</li>
      <li>
        <strong>Titolo originale:</strong>
        {{ cardItem.original_title || cardItem.original_name }}
      </li>
      <li>
        <strong>Lingua originale: </strong>
        <img
          v-if="flagImg(cardItem.original_language)"
          :src="require(`../assets/img/${cardItem.original_language}.png`)"
          :alt="cardItem.original_language"
        />
        <span v-else>{{ cardItem.original_language }}</span>
      </li>
      <li><strong>Voto:</strong> {{ cardItem.vote_average }}</li>
    </ul>
  </li>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      flags: ["it", "en"],
    };
  },
  props: {
    cardItem: Object,
  },
  methods: {
    flagImg(language) {
      return this.flags.includes(language);
    },
  },
};
</script>

<style scoped lang="scss">
.card {
  margin: 10px 0;
}

img {
  width: 20px;
}
</style>