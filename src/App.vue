<template>
  <div id="app">
    <WeatherMain />
  </div>
</template>

<script>
import WeatherMain from "./components/WeatherMain";

export default {
  name: "App",
  components: {
    WeatherMain,
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
#app {
  font-family: sans-serif;
}
</style>
