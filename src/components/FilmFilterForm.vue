<template lang="html">
  <div class="list">
    <!-- <form class="" v-on:submit.prevent>
      <select v-on:change="handleSelect" v-model="selectedFilm">
        <option disabled value="">Select a Film</option>
        <option v-for="film in films" :value="film">{{film.title}}</option>
      </select>
    </form> -->
    <p v-for="film in films" v-on:click="handleSelect(film)" class="item">{{film.title}}</p>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "film-filter-form",
  // data() {
  //   return {
  //     selectedFilm: ""
  //   }
  // },
  props: ['films'],
  methods: {
    handleSelect(film){
      // this.search = ""

      eventBus.$emit('film-selected', film)
    }
  }
}
</script>

<style lang="css" scoped>
  .list {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
  }

  .item:hover {
    cursor: pointer;
    text-decoration: underline;
  }

  .item:visited {
    text-decoration: underline;
  }
</style>
