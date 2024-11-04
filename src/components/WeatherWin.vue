<script lang="ts">
import DataFetch from './DataFetch.vue';
export default {
  name: 'App',
  components: {
    DataFetch
  },
  props: {
    lat: {
      type: Number,
      required: true
    },
    lon: {
      type: Number,
      required: true
    }
  },

  data(): { weatherData: { name: string; main: { temp: number; temp_min: number; temp_max: number; feels_like: number; humidity: number; pressure: number; }; sys: { country: string; }; dt: number; timezone: 0; time: number; weather: { icon: string; }[] }; iconMap: { [key: string]: string }; intlTimeZones: { [key: string]: string } } {
    return {
      weatherData: {
        name: '',
        main: {
          temp: 0,
          temp_min: 0,
          temp_max: 0,
          feels_like: 0,
          humidity: 0,
          pressure: 0,
        },
        sys: {
          country: '',
      
        },
        dt: 0,
        timezone: 0,
        weather: [
          {
            icon: ''
          }
        ],
        time: 0

      },
      iconMap: {
        '01d': 'fa-solid fa-sun',
        '01n': 'fa-solid fa-moon',
        '02d': 'fa-solid fa-cloud-sun',
        '02n': 'fa-solid fa-cloud-moon',
        '03d': 'fa-solid fa-cloud',
        '03n': 'fa-solid fa-cloud',
        '04d': 'fa-solid fa-cloud',
        '04n': 'fa-solid fa-cloud',
        '09d': 'fa-solid fa-cloud-showers-heavy',
        '09n': 'fa-solid fa-cloud-showers-heavy',
        '10d': 'fa-solid fa-cloud-sun-rain',
        '10n': 'fa-solid fa-cloud-moon-rain',
        '11d': 'fa-solid fa-bolt',
        '11n': 'fa-solid fa-bolt',
        '13d': 'fa-solid fa-snowflake',
        '13n': 'fa-solid fa-snowflake',
        '50d': 'fa-solid fa-smog',
        '50n': 'fa-solid fa-smog'
      },
      intlTimeZones: {
        '0': 'GMT',
        '3600': 'Europe/Paris',
        '7200': 'Europe/Athens',
        '10800': 'Europe/Moscow',
        '12600': 'Asia/Tehran',
        '14400': 'Asia/Dubai',
        '16200': 'Asia/Kabul',
        '18000': 'Asia/Karachi',
        '19800': 'Asia/Kolkata',
        '20700': 'Asia/Kathmandu',
        '21600': 'Asia/Dhaka',
        '23400': 'Asia/Yangon',
        '25200': 'Asia/Bangkok',
        '28800': 'Asia/Shanghai',
        '32400': 'Asia/Tokyo',
        '34200': 'Australia/Adelaide',
        '36000': 'Australia/Brisbane',
        '39600': 'Pacific/Norfolk',
        '43200': 'Pacific/Auckland'
        
      }
    }
  },
  computed: {
    localTime(): string {
      const dateOptions = {
        hour: 'numeric' as const, minute: 'numeric' as const, second: 'numeric' as const,
        timeZone: this.intlTimeZones[this.weatherData.timezone.toString()]
      }
      const dateFormatter = new Intl.DateTimeFormat('en-US', dateOptions);
      const dateFormatter2 = dateFormatter.format(new Date(this.weatherData.dt * 1000));
      return dateFormatter2;
    }
  },
  methods: {
    processMessage(data: any) {
      this.weatherData = data;
    }
  },
  mounted: function () {
    console.log('App component mounted.')
  }
}

</script>
  
<template>
<DataFetch :key="lat + ',' + lon" :lat="lat" :lon="lon" @dataFetched='processMessage' />
<div class="weather">
<v-card maxWidth="800px" minWidth="800px" class="weatherCard py-4">
  <v-card-item ><v-card-title>{{weatherData.name}}, {{ weatherData.sys.country }}</v-card-title><v-card-subtitle>{{localTime}}</v-card-subtitle></v-card-item>
    <v-card-text class="py-1">
      <v-row align="center" no-gutters>
        <v-col class="text-h2" cols="6">
            <div class="flex">
              {{ weatherData.main.temp }}°C
              <v-list>
                <v-list-item>
                  <v-list-item-subtitle>Humidity: {{ weatherData.main.humidity }}%</v-list-item-subtitle>
                  <v-list-item-subtitle>Pressure: {{ weatherData.main.pressure }} hPa</v-list-item-subtitle>
                </v-list-item>
              </v-list>
            </div>
          <v-card-subtitle>High: <b>{{ weatherData.main.temp_max }}°C</b> | Min: <b>{{ weatherData.main.temp_min }}°C</b></v-card-subtitle>
          <v-card-subtitle class="text-h7">Feels like: <b>{{ weatherData.main.feels_like }}°C</b></v-card-subtitle>
        </v-col>
        <v-col class="text-right" cols="6">
          <v-icon :icon="iconMap[weatherData.weather[0].icon]" size="88" class="mx-10"></v-icon>
          <v-card-text></v-card-text>
        </v-col>
      </v-row>
    </v-card-text>
</v-card>
</div>
</template>
<style>
.weather {
  display: flex;
  width: 100vw;
  height: 100vh;
  justify-content: center;
  align-items: center;

}
.flex {
  display: flex;
  flex-direction: row;
  justify-content: start;
  align-items: center;
}
.flex2 {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>


