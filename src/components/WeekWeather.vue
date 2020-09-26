<template>
  <div class="WeekWeather">
    <DayWeather v-for="day in weeklyWeather" :key="day.id" v-bind="day" />
  </div>
</template>

<script>
import DayWeather from "./DayWeather";
export default {
  name: "WeekWeather",
  props: {
    weeklyWeather: [],
  },
  components: { DayWeather },
};
</script>

<style></style>
