<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/pokedex.jpg" alt="">
      <h4 class="is-size-4">POKEDEX - TESTE</h4>
      <input type="text" placeholder="Search by name" v-model="search" class="input is-rounded">
      <button type="button" class="button is-fullwidth is-success" id="btnSearch" @click="searchResult">Search</button>
      <div v-for="(poke,index) in filteredPokemons" :key="poke.url">
        <Pokemon :num="index+1" :name="poke.name" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then((response => {
      this.pokemons = response.data.results;
      this.filteredPokemons = response.data.results;
    }))
  },
  data(){
    return{
      pokemons: [],
      filteredPokemons: [],
      search: '',
    }
  },
  components: {
    Pokemon,
  },
  methods: {
    searchResult: function(){
      if(this.search == '' || this.search == ' '){
        this.filteredPokemons = this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.search)
     }
    }
  },
  computed: {
    // searchResult: function(){
    //   if(this.search == '' || this.search == ' '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.search)
    //   }
    // }
  }
}

</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  #btnSearch{
    margin-top: 2%;
  }
</style>
