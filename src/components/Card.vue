<template>
  <div class="card position-relative mx-3">
    <img
      class="poster card-img-top position-absolute"
      v-if="cardItem.poster_path"
      :src="uriPoster + cardItem.poster_path"
      :alt="cardItem.title || cardItem.name"
    />
    <img
      class="poster card-img-top position-absolute"
      v-else
      src="../assets/img/poster-placeholder.png"
      alt="no poster"
    />
    <div class="card-body">
      <ul class="p-0">
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
          <span class="text-uppercase" v-else>{{
            cardItem.original_language
          }}</span>
        </li>
        <li>
          <strong>Descrizione: </strong>
          <span>{{ cardItem.overview }}</span>
        </li>
        <li>
          <strong>Voto:</strong>
          <i
            v-for="(num, index) in newVote"
            :key="num + '-' + index"
            class="fas fa-star red-star"
          ></i>
          <i
            v-for="num in 5 - newVote"
            :key="num"
            class="fas fa-star white-star"
          ></i>
        </li>
      </ul>
    </div>
  </div>
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
  computed: {
    newVote() {
      return Math.ceil(this.cardItem.vote_average / 2);
    },
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
  border: none;
  background-color: transparent;
}

.poster {
  z-index: -1;
}

.card-body {
  overflow-y: auto;
  ul {
    color: white;
    list-style-type: none;
    strong {
      color: red;
    }
  }
}

img.flag {
  width: 25px;
  vertical-align: middle;
}

.red-star {
  color: red;
}

.white-star {
  color: white;
}
</style>