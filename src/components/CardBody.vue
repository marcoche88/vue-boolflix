<template>
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
        <span v-if="cardItem.overview">{{ cardItem.overview }}</span>
        <span v-else>...</span>
      </li>
      <li>
        <strong>Voto: </strong>
        <i
          v-for="(num, index) in newVote"
          :key="num + '-' + index"
          class="fas fa-star"
        ></i>
        <i v-for="num in 5 - newVote" :key="num" class="far fa-star"></i>
      </li>
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
.card-body {
  display: none;
  overflow-y: auto;
  ul {
    font-size: 14px;
    color: white;
    list-style-type: none;
    li {
      margin: 10px 0;
    }
    strong {
      color: red;
    }
  }
}

.card:hover .card-body {
  display: block;
  background-color: rgba(#202020, 0.7);
}

img.flag {
  width: 25px;
  vertical-align: middle;
}

i.fas {
  color: red;
}
</style>