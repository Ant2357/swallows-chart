
<template>
  <div id="contents">
    <GChart
      :settings="chartSettings"
      type="GeoChart"
      :data="chartData"
      :options="chartOptions"
    />
  </div>
</template>

<script>
import { GChart } from 'vue-google-charts';
import swallowsPlayers from '@/assets/json/SwallowsPlayers.json'

const chartDataMap = swallowsPlayers
  .reduce((accMap, player) =>
    accMap.has(player.hometown) 
      ? accMap.set(player.hometown, accMap.get(player.hometown) + 1) // count++
      : accMap.set(player.hometown, 1) // default count
  , new Map([['県', '選手人数']]));

const chartDataValue = [...chartDataMap];

export default {
  components: {
    GChart
  },
  data() {
    return {
      chartSettings: {
        packages: ['geochart'],
        'mapsApiKey': 'XXXXXXX'
      },
      chartData: chartDataValue,
      chartOptions: {
        region: 'JP',
        resolution: 'provinces',
        displayMode: 'regions',
      }
    };
  }
}
</script>
