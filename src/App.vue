<template>
  <div id="App">
    <div v-for="(poke, index) in pokemons" :key="index">
      <Pokemons :name="poke.name" :url="poke.url" :num="index + 1"/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemons from "./components/Pokemons"

export default {
  name: 'App',
  data() {
    return {
      pokemons: []
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then(res => {
        this.pokemons = res.data.results;
      });
  },
  components: {
    Pokemons,
  }
}
</script>

<style>
#App {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
