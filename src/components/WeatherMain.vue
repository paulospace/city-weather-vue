<template>
  <div class="WeatherMain">
    <button v-on:click="getWeather(testCity.lat, testCity.lon)">
      Get Weather Data
    </button>
    <div v-if="currentWeather">
      <p>
        {{ currentWeather.temp }}
        <CurrentWeather
          v-bind:current-temp="currentWeather.temp"
          v-bind:date="currentWeather.dt"
          v-bind:wind-speed="currentWeather.wind_speed"
          v-bind:humidity="currentWeather.humidity"
        ></CurrentWeather>
      </p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CurrentWeather from "./CurrentWeather";

const openWeatherApiKey = "f1c6f3727e6bebbb08e546ce1dc2236a";

/**
 * Get weather data from OpenWeatherMaps One Call API
 *
 * A Api de one call receive the parameters:
 * {
 *  appid: the api key,
 *  lat: latitude,
 *  lon: longitude,
 *  units: the unit of measurement, default being kelvin,
 *  lang: language, defaults to english
 * }
 *
 * @param {String} lat the selected location latitude
 * @param {String} lon the selected longitude
 * @param {String} apiKey The OpenWeatherMaps ApiKey
 */

const getCurrentWeather = (lat, lon, apiKey) => {
  return axios({
    method: "get",
    url: "https://api.openweathermap.org/data/2.5/onecall",
    params: {
      appid: apiKey,
      lat: lat,
      lon: lon,
      units: "metric",
      lang: "en",
    },
  })
    .then((response) => {
      console.log(response.data);
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
      currentWeather: null,
      dailyWeather: null,
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
    getWeather: function(lat, lon) {
      getCurrentWeather(lat, lon, openWeatherApiKey).then((weather) => {
        this.currentWeather = weather.current;
        this.dailyWeather = weather.daily;
      });
    },
  },
  components: { CurrentWeather },
};
</script>

<style></style>
