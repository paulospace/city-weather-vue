<template>
  <div class="LocationSearch">
    <input v-model="locationSearchInput" type="text" />
    <button @click="searchForLocation(locationSearchInput)">Search</button>
    <div v-if="locationMatches">
      <div
        v-for="match in locationMatches"
        :key="match.id"
        @click="
          $emit('location-click', {
            lon: match.center[0],
            lat: match.center[1],
            name: match.place_name,
          })
        "
      >
        <p class="location-match_name">
          {{ match.place_name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

const apiKey =
  "pk.eyJ1Ijoic3BhY2VhcmNoZXIiLCJhIjoiY2tmOWFuMGZwMGszbzJycnFmcDJsYzBveSJ9.-995FXHbG6UJIIvne3PPRQ";

/**
 * Get city matches from the Mapbox Geolocation API
 *
 * @param {String} query
 * @param {String} apiKey
 */
function getLocationMatches(query, apiKey) {
  return axios({
    baseURL: "https://api.mapbox.com/geocoding/v5/mapbox.places/",
    url: `${escape(query)}.json`,
    params: {
      access_token: apiKey,
      autocomplete: true,
      types: "place",
    },
  })
    .then((response) => {
      return response.data;
    })
    .catch((error) => {
      console.log(error);
    });
}
export default {
  name: "LocationSeach",
  props: {
    previousLocations: Array,
    onLocationSearch: Function,
  },
  data: function() {
    return {
      locationSearchInput: "",
      locationMatches: null,
    };
  },
  methods: {
    searchForLocation: function(query) {
      if (!query) return;
      getLocationMatches(query, apiKey).then((matches) => {
        this.locationMatches = matches.features;
      });
    },
    onLocationClick: function(match) {
      this.locationClick(match.center[0], match.center[1]);
    },
  },
};
</script>

<style></style>
