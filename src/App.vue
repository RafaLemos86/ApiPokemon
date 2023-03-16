<template>
  <div v-for="(poke, index) in pokemons" :key="index">
      <pokemon :name="poke.name" :url="poke.url" :num="poke.num"/> 
  </div>
</template>

<script>
import axios from 'axios';
import pokemon from './components/pokemon.vue';

export default {
  name: 'App',
  data(){
    return {
      pokemons: []
    }
  },  
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
    }).catch(err => {
      console.log(err)
    })
  },
  components: {
    pokemon
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
</style>
