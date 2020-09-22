<template>
  <div class="WeekWeather"></div>
</template>

<script>
import DayWeather from "./DayWeather";
export default {
  name: "WeekWeather",
  props: {
    weeklyWeather: Array,
  },
  components: { DayWeather },
};
</script>

<style></style>
