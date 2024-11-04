<script setup lang="ts">
import axios from 'axios';

</script>
<script lang="ts">
export default {
    
  name: 'GeoPos',
  data() {
    return {
        geoData: {
        lat: 0,
        lon: 0
      },
        cityName: '',
    }
  },
  methods: {
    searchLoc(cityName: any) {
    console.log(cityName)
    let link = 'http://api.openweathermap.org/geo/1.0/direct?q=' + cityName + '&limit=1&appid=16e6b5c9b9cfc2b5bb0a6003773e9ced'
    axios
      .get(link)
      .then(response => {
        console.log(response.data), console.log(response.status), this.$emit('geoFetched', response.data), this.cityName = ''})
    }
  },
  mounted() {
    
  }
}
</script>
<template>
  <v-form @submit.prevent="searchLoc(cityName)">
    <v-text-field label="City name" v-model="cityName"></v-text-field>
  </v-form>
  
</template>