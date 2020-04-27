<template lang="html">
  <div>
    <h1>Films</h1>
    <film-filter-form :films="films" />
    <film-detail v-if="selectedfilm" :film="selectedfilm"/>
  </div>
</template>

<script>
import filmFilterForm from './components/filmFilterForm.vue'
import filmDetail from './components/filmDetail.vue'
import {eventBus} from './main.js';

export default {
  data(){
    return {
      films: [],
      selectedfilm: null
    }
  },
  components: {
    "film-filter-form": filmFilterForm,
    "film-detail": filmDetail
  },
  mounted(){
    fetch('https://swapi.dev/api/films/')
    .then(res => res.json())
    .then(data => this.films = data.results)

    eventBus.$on('film-selected', (film) => {
      this.selectedfilm = film
    })
  }
}
</script>

<style lang="css" scoped>
h1 {
  text-align: center;
  color: #333;
}
</style>
