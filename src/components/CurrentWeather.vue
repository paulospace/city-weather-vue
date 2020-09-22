<template>
  <div class="CurrentWeather">
    <h1 class="current-temp">{{ currentTemp }}°C</h1>
    <div class="other-data">
      <div class="data-humidity">Humidity: {{ humidity }}%</div>
      <div class="data-wind">Wind: {{ windSpeedKM }} km/h</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CurrentWeather",
  props: [
    "currentTemp",
    "date",
    "windSpeed",
    "humidity",
    "pop",
    "desc",
    "feelsLike",
  ],
  data: function() {
    return { windSpeedKM: Math.floor(this.windSpeed * 3.6) };
  },
};
</script>

<style></style>
