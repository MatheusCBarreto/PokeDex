<template>
  <div id="app">
    <h1 class=" column is-half is-offset-one-quarter is-size-2">PokeDex</h1>
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-rounded busca" type="text" placeholder="Buscar pokemon" v-model="busca">
      <button class="button is-dark busca buscaBtn" id="busca" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemons :name="poke.name" :url="poke.url" :num="index + 1" />
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
      pokemons: [],
      filteredPokemons: [],
      busca: '',
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then(res => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      });
  },
  components: {
    Pokemons,
  },
  methods: {
    buscar() {
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == " ") {
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name === this.busca)
      }
    }
  }
  //computed: {
    /*
    resultadoBusca: function() {
      if(this.busca == '' || this.busca == " ") {
        return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }*/
  //}
}
</script>

<style>
  .busca {
    margin-bottom: 2%
  }

  .buscaBtn {
    border-radius: 10%;
  }
</style>
