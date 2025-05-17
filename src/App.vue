<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
        <img src="./assets/logo.png" alt="">
        <hr>
        <h4 class="is-size-1">Pokedexx</h4>
      <div v-for="(poke, index) in pokemons" :key="index">
        <PokemonInfo :name="poke.name" :num="poke.num" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PokemonInfo from "./components/PokemonInfo.vue";

export default {
  name: "App",
  data() {
    return {
      pokemons: [],
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
      .then((res) => {
        console.log("Pegou lista de Requisição básica!");
        this.pokemons = res.data.results;
      });
  },
  components: {
    PokemonInfo,
  },
};
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
