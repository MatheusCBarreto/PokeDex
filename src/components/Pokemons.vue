<template>
  <div id="pokemon">
    <div class="card">
      <div class="card-image">
      <figure class="">
        <img :src="currentImg" alt="Placeholder image">
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ num }} {{ upper(name)}}</p>
          <p class="subtitle is-6">Tipo: {{ pokemon.type }}</p>
          <button @click="mudarSprite" class="button is-dark">Mudar posição do pokemon</button>
        </div>
      </div>
      <div class="content">
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import axios from "axios";


export default {
  created: function() {
    axios.get(this.url).then(res => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      // tratando da exibição da imagem
      this.currentImg = this.pokemon.front;

      console.log(this.pokemon);
    })
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        type: '',
        front: '',
        back: '',
      }
    }
  },
  props: {
    num: Number,
    name: String,
    url: String
  },
  methods: {
    upper: function(value) {
      let newName = value[0].toUpperCase() + value.slice(1);
      return newName
    },
    mudarSprite() {
      if(this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    }
  }
}
</script>

<style>
  #pokemon {
    margin-top: 1%;
  }
</style>