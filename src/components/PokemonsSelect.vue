<template lang="html">
  <div>
    <select @change=onChange() v-model="selectedPokemon">
      <option v-for="(pokemon, index) in pokemons" :value="pokemon" :key="index">{{pokemon.name}}</option>
    </select>
  </div>

</template>

<script>
import { eventBus } from '../main.js';


export default {
  name: 'pokemons-select',
  props: ['pokemons','pokemon'],



  methods: {

  onChange(){
      eventBus.$emit('pokemon-selected', this.selectedPokemon)

  }

  }


}
</script>
