<template>
  <div class="column is-half is-offset-one-quarter">
    <h1 class="title">Criado Por:</h1>
  <h2 class="subtitle"> 
    <a href="https://www.linkedin.com/in/rafael-lemos-a433a31a1/" style="color: black;"  target="_blank">
    Rafael Lemos
    </a>
  </h2>

    <div v-for="(poke, index) in pokemons" :key="index">
      <AllPokemons :name="poke.name" :url="poke.url" :num="index"/> 
      <br>
    </div>

  </div>
</template>

<script>
// axios para consumir API
import axios from 'axios';
import AllPokemons from './components/AllPokemons.vue';

export default {
  name: 'App',
  data(){
    return {
      // inicializando lista de pokemons
      pokemons: []
    }
  },  
  // essa funcao é executada sempre que o codigo inicia
  // coletando os pokemons da API e inserindo na lista "pokemons"
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
      this.pokemons = res.data.results
    }).catch(err => {
      console.log(err)
    })
  },
  components: {
    AllPokemons
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
