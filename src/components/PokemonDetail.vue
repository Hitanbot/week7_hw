
<template lang="html">


  <div>

  <div v-if='pokemonDetails'>
    <h3>{{pokemonDetails.name}}</h3>
    <h4>Stats: </h4>

    <p> Hp : {{pokemonDetails.stats[0].base_stat}}</p>
    <p> Attack : {{pokemonDetails.stats[1].base_stat}}</p>
    <p> Defence : {{pokemonDetails.stats[2].base_stat}}</p>
    <p> Special-Attack : {{pokemonDetails.stats[3].base_stat}}</p>
    <p> Special-Defence : {{pokemonDetails.stats[4].base_stat}}</p>
    <p> Speed : {{pokemonDetails.stats[5].base_stat}}</p>
    <!-- gonna graph this next -->


    <img :src="pokemonDetails.sprites.front_default"/>


    </div>
  </div>
</template>

<script>



export default {
  name: 'pokemon-detail',
  props: ['pokemon','pokemonDetails'],
  components: {

  }
}

</script>

<style lang="css" scoped>
</style>
