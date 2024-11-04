<script lang="ts">
import axios from 'axios';
export default {
  name: 'DataFetch',
  props: {
    lat: Number,
    lon: Number,
  },
  data() {
    return {
    };
  },
  methods: {
  fetchData() {
    const link = 'https://api.openweathermap.org/data/2.5/weather?lat=' + this.lat + '&lon=' + this.lon + '&units=metric&appid=16e6b5c9b9cfc2b5bb0a6003773e9ced';
    axios
      .get(link)
      .then(response => {
        console.log(response.data);
        this.$emit('dataFetched', response.data);
      });
  }
},
mounted() {
  this.fetchData();
}
};

</script>
<template>
  <div>
  </div>
</template>