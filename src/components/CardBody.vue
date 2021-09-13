<template>
  <div class="card-body">
    <ul class="p-0 text-white">
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
        <span v-if="cardItem.overview">{{ cardItem.overview }}</span>
        <span v-else>...</span>
      </li>
      <li>
        <strong>Voto: </strong>
        <i
          v-for="(num, index) in newVote"
          :key="num + '-' + index"
          class="fas fa-star text-red"
        ></i>
        <i v-for="num in 5 - newVote" :key="num" class="far fa-star"></i>
      </li>
      <li><strong>Genere: </strong> {{ getGenre() }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "CardBody",
  data() {
    return {
      flags: ["it", "en"],
    };
  },
  props: {
    cardItem: Object,
    genres: Array,
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
    getGenre() {
      if (!this.cardItem.genre_ids.length) return "N.A.";
      let genreList = [];
      this.cardItem.genre_ids.forEach((genre_id) => {
        this.genres.forEach((genre) => {
          if (genre_id === genre.id) {
            genreList.push(genre.name);
          }
        });
      });

      return genreList.join(", ");
    },
  },
};
</script>

<style scoped lang="scss">
@import "../scss/_vars.scss";

.card-body {
  display: none;
  overflow-y: auto;
  ul {
    font-size: 14px;
    list-style-type: none;
    li {
      margin: 10px 0;
    }
    strong {
      color: $primary-title-color;
    }
  }
}

.card:hover .card-body {
  display: block;
  background-color: rgba($secondary-bg-color, 0.7);
}

img.flag {
  width: 25px;
  vertical-align: middle;
}
</style>