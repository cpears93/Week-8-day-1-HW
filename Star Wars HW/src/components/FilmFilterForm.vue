<template lang="html">
  <form v-on:submit.prevent>
    <input type="text" v-model="search" placeholder="search for film..." v-on:keyup="searchForfilm">
    <select v-on:change="handleSelect" v-model="selectedfilm">
      <option disabled value="">Select a film...</option>
      <option v-for="film in films" :value="film">{{film.name}}</option>
    </select>
  </form>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "film-filter-form",
  data(){
    return {
      "search": "",
      "selectedfilm": {},
    }
  },
  props: ["films"],
  methods: {
    searchForfilm(){
      let foundfilm = this.films.find((film) => {
        return film.name.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      this.selectedfilm = foundfilm

      eventBus.$emit('film-selected', this.selectedfilm)
    },
    handleSelect(){
      this.search = ""
      eventBus.$emit('film-selected', this.selectedfilm)
    }
  }
}
</script>

<style lang="css" scoped>
form{
  text-align: center;
  margin: 40px 0;
}

select, input[type="text"]{
  font-size: 18px;
}

select {
  margin-left: 20px;
}
</style>
