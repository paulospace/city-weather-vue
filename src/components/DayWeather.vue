<template>
  <div class="DayWeather">
    <div class="daily-day">{{ Date(date) }}</div>
    <div class="daily-temp">{{ temp }}°C</div>
    <div class="daily-minmax">Min:{{ tempMin }} Max: {{ tempMax }}</div>
    <div class="daily-humidity">Humidity: {{ humidity }}></div>
    <div class="daily-wind">Wind: {{ windSpeed }} km/h</div>
  </div>
</template>

<script>
export default {
  name: "DayWeather",
  props: {
    temp: [String, Number],
    tempMax: [String, Number],
    tempMin: [String, Number],
    windSpeed: [String, Number],
    humidity: [String, Number],
    pop: [String, Number],
    date: Number,
    icon: String,
    desc: String,
  },
};
</script>

<style></style>
