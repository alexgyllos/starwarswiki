<template lang="html">
  <div v-if="film" class="filmDetail">
    <p>{{film.title}} - Episode: {{film.episode_id}}</p>
    <p>Release Date: {{film.release_date | fixDate}}</p>
    <p>Director: {{film.director}}</p>
    <hr>
    <character-list v-if="characters.length" :characters="characters"></character-list>
  </div>
</template>

<script>
import CharacterList from './CharacterList.vue'
var moment = require('moment');
moment().format();

export default {
  name: 'film-detail',
  props: ['film'],
  components: {
    'character-list': CharacterList
  },
  data() {
    return {
      characters: []
    }
  },
  methods: {
    getCharacters: function() {
      const characterPromises = this.film.characters.map((characterUrl) => {
        return fetch(characterUrl).then(res => res.json())
      })
      Promise.all(characterPromises)
      .then(data => this.characters = data)
      // console.log(characterPromises);
    }
  },
  mounted() {
    this.getCharacters();
  },
  watch: {
    film: function() {
      this.getCharacters();
    }
  },
  filters: {
    fixDate: function(date) {
      return moment(date, 'YYYY-MM-DD').format('Do MMM YYYY')
    }
  }
}
</script>


<style lang="css" scoped>
</style>
