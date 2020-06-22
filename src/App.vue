<template>
  <div>

  <h1>Pokemon</h1>
    <div class="main-container">
      <pokemons-select :pokemons='pokemons'></pokemons-select>
      <pokemon-detail :pokemonDetails='pokemonDetails'></pokemon-detail>
      <!-- <pokemon-stats :pokemonDetails='pokemonDetails'></pokemon-stats> -->
      <!-- <button v-if="!favouritepokemons.includes(selectedpokemon)" v-on:click="addToFavourites">Add pokemon to Favorites</button>
      <h2>Favorites</h2>
      <pokemons-list :pokemons='favouritepokemons'></pokemons-list> -->
    </div>
  </div>
</template>

<script>
// import PokemonGraph from './components/PokemonGraph.vue';
import PokemonsSelect from './components/PokemonsSelect.vue';
import PokemonDetail from './components/PokemonDetail.vue';
// import PokemonsList from './components/PokemonsList.vue';
import { eventBus } from './main.js';

export default {
  name: 'App',
  data(){
  return {
    pokemons: [],
    selectedPokemon: null,
    favouritePokemons: [],
    next: null,
    pokemonDetails: null
    };
  },
  methods:{

      },
  mounted(){
     fetch('https://pokeapi.co/api/v2/pokemon-species/?offset=0&limit=151')//gen 1 pokemon though i can do more
    .then(res => res.json())
    .then(data => {
      data['results'].forEach((pokemon) => {
        this.pokemons.push(pokemon)
      });

      this.next=data['next'];


    })




    // while (this.next !== null) {
    //   fetch(this.next)
    //   .then(res => res.json())
    //   .then(data => {
    //     data['results'].forEach((pokemon) => {
    //       this.pokemons.push(pokemon)
    //     });
    //
    //     this.next=data['next'];
    //
    //   })
    //
    // }

    eventBus.$on('pokemon-selected', (pokemon) => {
    this.selectedPokemon = pokemon;
    console.log(pokemon)
    fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokemons.indexOf(this.selectedPokemon)+1}/`)
   .then(res => res.json())
   .then(data => {
     this.pokemonDetails=data;
   console.log(this.pokemonDetails)})

  })

  // eventBus.$on('pokemon', (pokemon) => {
  // this.favouritePokemons=this.favouritePokemons.filter(item => item.name !== pokemon.name);
  // console.log(pokemon)
// })
  },


  // addToFavourites: function(){
  //       this.favouritePokemons.push(this.selectedPokemon)
  //     }

  components: {
    'pokemons-select': PokemonsSelect,
    'pokemon-detail': PokemonDetail
    // 'pokemons-stats': PokemonsGraph

    // 'pokemons-list': PokemonsList
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
