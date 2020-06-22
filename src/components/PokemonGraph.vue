<template lang="html">
  <GChart
    v-if="chartData"
    :type="BarChart"
    :data="chartData"
    :options="chartOptions"
  />
</template>

<script>
import { GChart } from 'vue-google-charts'


export default {
  name: 'pokemon-stats',
  data(){
    return {
      chartOptions: {
        width: 800,
        height: 240,
        title: 'Base stats',
        colors: ['#084887', '#f58a07', '#f9ab55', '#f7f5fb', '#909cc2', '#C1BB8F']
      },
      chartType: "ColumnChart"
    }
  },
  props: ['pokemonDetails'],
  components : {
    GChart
  },
  // mounted(){
  //   eventBus.$on('chart-select', (chartType) => {
  //     this.chartType = chartType
  //   })
  // },
  computed: {
    chartData: function(){
      if(this.pokemonDetails){
        const chartData = [this.pokemonDetails.stats[0].base_stat,
        this.pokemonDetails.stats[1].base_stat,
        this.pokemonDetails.stats[2].base_stat,
        this.pokemonDetails.stats[3].base_stat,
        this.pokemonDetails.stats[4].base_stat,
        this.pokemonDetails.stats[5].base_stat
      ]
        return chartData
      }
      return null
    }
  }
}
</script>

<style lang="css" scoped>
</style>
