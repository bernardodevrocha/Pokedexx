<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
        <img src="./assets/logo.png" alt="">
        <hr>
        <h4 class="is-size-1">Pokedex</h4>
        <input class="input is-rounded" type="text" v-model="busca" placeholder="Buscar Pokemon pelo nome" />
        <button class="button is-fullwidth is-success" id="buscaButton" @click="buscar">Buscar</button>
        <div v-for="(poke) in filteredPokemons" :key="poke.url">
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
      filteredPokemons: [],
      busca: ''
    };
  },
  created: function () {
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0")
      .then((res) => {
        console.log("Pegou lista de Requisição básica!");
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.result;
      });
  },
  components: {
    PokemonInfo,
  },
  methods:{
    buscar: function(){
      this.filteredPokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  computed: {
    // resultadoBusca: function() {
    //   if(this.busca == '' || this.busca == ' '){
    //     return this.pokemons;
    //   }else{
    //     return this.pokemons.filter(pokemon => pokemon.name == this.busca);
    //   }
    // }
  }
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

#buscaButton{
  margin-top: 15px;
}
</style>
