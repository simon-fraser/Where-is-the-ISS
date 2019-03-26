<template>
  <div id="app">
    <header>
      <h1>
        <a href="https://en.wikipedia.org/wiki/International_Space_Station" target="_blank">
          International Space Station
          <img src="./assets/ext.svg" alt="International Space Station Wikipedia" class="ext">
        </a>
      </h1>
      <h2>Current Location</h2>
    </header>
    <Map :position="position" />
  </div>
</template>

<style>
  body {
    margin: 0px;
    font-family: Helvetica, Verdana, sans-serif;
  }

  header .ext {
    padding-top: 10px;
    vertical-align: top;
    width: 10px;
  }
</style>

<script>
import Map from './components/Map.vue'
import L from 'leaflet'
import { setInterval } from 'timers';

export default {
  name: 'app',
  components: {
    Map
  },

  data () {
    return {
      position: L.latLng(0, 0)
    }
  },
  methods: {
    getPOS () {
      setInterval(() => {
        fetch('http://api.open-notify.org/iss-now.json')
          .then((response) => {
            return response.json()
          })
          .then((json) => {
            if (json.message === "success") this.position = L.latLng(json.iss_position.latitude, json.iss_position.longitude)
          })
      }, 2200)
    }
  },
  mounted: function () {
    this.getPOS()
  },
}
</script>


