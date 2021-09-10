<template>
  <li class="card">
    <ul>
      <li>
        <img
          class="poster"
          v-if="cardItem.poster_path"
          :src="uriPoster + cardItem.poster_path"
          :alt="cardItem.title || cardItem.name"
        />
        <img
          class="poster"
          v-else
          src="../assets/img/poster-placeholder.png"
          alt="no poster"
        />
      </li>
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
          class="flag"
        />
        <span class="no-flag" v-else>{{ cardItem.original_language }}</span>
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
      uriPoster: "https://image.tmdb.org/t/p/w342",
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
  margin: 40px 0;
}

ul li {
  list-style-type: none;
}

img.poster {
  width: 100px;
}

img.flag {
  width: 20px;
}

.no-flag {
  text-transform: uppercase;
}
</style>