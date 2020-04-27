<template lang="html">
  <div class="container">
    <div class="content">

      <h1 class="nav">Star Wars Wiki</h1>
      <hr>
      <film-filter-form class="nav" :films="films"></film-filter-form>
      <hr>
      <film-detail v-if="selectedFilm" :film="selectedFilm"></film-detail>
    </div>
  </div>
</template>

<script>
import FilmFilterForm from './components/FilmFilterForm.vue'
import {eventBus} from './main.js';
import FilmDetail from './components/FilmDetail.vue'

export default {
  name: "app",
  data() {
    return {
      films: [],
      selectedFilm: null
    }
  },
  mounted(){
    fetch('https://swapi.dev/api/films/')
    .then(res => res.json())
    .then(data => this.films = data.results)

    eventBus.$on('film-selected', (film) => {
      this.selectedFilm = film
    })
  },
  components: {
    'film-filter-form': FilmFilterForm,
    'film-detail': FilmDetail
  }
}
</script>

<style lang="css" scoped>
  .container {
    /* display: flex;
    flex-direction: column; */
    /* justify-content: center; */
    align-items: center;
    /* background-image: url("https://images.unsplash.com/photo-1587676105543-434b44786174?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=582&q=80"); */
    background-color: rgba(0, 0, 0, 0.9);
    border-radius: 5px;
    width: 60%;
    height: 100%;
    margin: auto;
    background-repeat: no-repeat;
    background-size: cover;
    background-attachment: fixed;
    /* opacity: 0.8; */
  }

  .nav {
    /* text-align: left; */
  }

  .content {
    /* display: flex;
    flex-direction: column; */
    /* flex-shrink: 0; */
    color: rgba(245, 203, 92, 1);
    height: 100%;
    padding: 3%;
    /* justify-content: center; */
    text-shadow: 1px 0 1px #46494c;
    text-align: justify;
    margin: auto;
  }

  select {
    background: black;
  }
</style>

<style>
  html{
    background-image: url("https://images.unsplash.com/photo-1578374173703-3b306567209a?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=2886&q=80");
    background-size: cover;
    background-repeat: no-repeat;
    width: 100vw;
    height: 100vh;
    background-attachment: fixed;
    font-family: 'Staatliches', cursive;
    font-size: 1.1em;
    /* font-size: 1.5vw; */
    user-select: none;
  }
</style>
