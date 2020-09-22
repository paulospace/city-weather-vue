<template>
  <div class="WeatherMain">
    <LocationSearch @location-click="changeLocation" />
    <button v-on:click="getWeather(currentLocation || testCity)">
      Get Weather Data
    </button>
    <div v-if="currentWeather">
      <CurrentWeather
        v-bind:current-temp="currentWeather.temp"
        v-bind:date="currentWeather.dt"
        v-bind:wind-speed="currentWeather.wind_speed"
        v-bind:humidity="currentWeather.humidity"
      ></CurrentWeather>
      <div v-if="dailyWeather">
        <WeekWeather />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import CurrentWeather from "./CurrentWeather";
import WeekWeather from "./WeekWeather";
import LocationSearch from "./LocationSearch";

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
      currentLocation: null,
      pastLocations: [],
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
    getWeather: function(location) {
      getCurrentWeather(location.lat, location.lon, openWeatherApiKey).then(
        (weather) => {
          this.currentWeather = weather.current;
          this.dailyWeather = weather.daily;
        }
      );
    },
    changeLocation(location) {
      console.log(location);
      if (this.currentLocation) this.pastLocations.push(this.currentLocation);
      this.currentLocation = location;
    },
  },
  components: { CurrentWeather, WeekWeather, LocationSearch },
};
</script>

<style></style>
