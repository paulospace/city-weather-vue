<template>
  <div class="WeatherMain">
    <button v-on:click="getWeather(testCity)">Get Weather Data</button>
  </div>
</template>

<script>
import axios from "axios";

const openWeatherApiKey = "f1c6f3727e6bebbb08e546ce1dc2236a";

/**
 * Get weather data from OpenWeatherMaps One Call API
 *
 * @param {Object} location A Object containing lat(latitude) and lon(longitude) float numbers
 * @param {String} apiKey The OpenWeatherMaps ApiKey
 */
const getCurrentWeather = (location, apiKey) => {
  return axios({
    method: "get",
    url: "https://api.openweathermap.org/data/2.5/onecall",
    params: {
      appid: apiKey,
      lat: location.lat,
      lon: location.lon,
    },
  })
    .then((response) => {
      console.log(response);
      return response.data;
    })
    .catch((error) => console.log(error));
};
export default {
  name: "WeatherMain",
  data: function() {
    return {
      currentLocation: String,
      pastLocation: Array,
      currentWeather: Object,
      testCity: {
        lat: "-23.5489",
        lon: "-46.6388",
        name: "São Paulo",
        state: "São Paulo",
        country: "Brasil",
      },
    };
  },
  methods: {
    getWeather: function(location) {
      getCurrentWeather(location, openWeatherApiKey).then(
        (weather) => (this.currentWeather = weather)
      );
    },
  },
};
</script>

<style></style>
