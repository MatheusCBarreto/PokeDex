<template>
  <div id="app">
    <h1 class=" column is-half is-offset-one-quarter is-size-2">PokeDex</h1>
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in pokemons" :key="index">
      <Pokemons :name="poke.name" :url="poke.url" :num="index + 1"/>
    </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemons from "./components/Pokemons"

export default {
  name: 'app',
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

</style>
