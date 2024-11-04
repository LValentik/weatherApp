<script lang="ts">
import WeatherWin from './components/WeatherWin.vue';
import GeoPos from './components/GeoPos.vue';
export default {
  name: 'App',
  data() {
    return {
      geoPosition: {
        lat: 50.0875,
        lon: 14.4213,
      },
    }

  },
  components: {
    WeatherWin,
    GeoPos
  },
  methods: {
    processMessage(data: any) {
      this.geoPosition.lat = data[0].lat;
      this.geoPosition.lon = data[0].lon;
    }
  },
}


</script>

<template>
<GeoPos @geoFetched="processMessage"/>
<WeatherWin :key="geoPosition.lat + ',' + geoPosition.lon" :lat="geoPosition.lat" :lon="geoPosition.lon"/>
</template>
