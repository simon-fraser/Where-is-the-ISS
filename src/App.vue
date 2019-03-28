<template>
  <div id="app">
    <header class="app-head container grid-md">
      <h1><a href="https://en.wikipedia.org/wiki/International_Space_Station" title="Link to Wikipedia Page" target="_blank">International Space Station</a></h1>
      <p>The International Space Station is such a amazing experiment, This application shows data from a couple of live feed sources and some additonal interesting information. enjoy :)</p>

      <hr>
    </header>

    <Map :position="position" />
    <Feed />
    <!-- <Details /> -->

  </div>
</template>

<style>
  html,
  body {
    height: 100%;
  }

  body {
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    background-color: #f3f3f3;
    color: #555;
    font-size: 14px;
    font-family: 'Montserrat', Helvetica, Verdana, sans-serif;
    font-weight: 300;
    margin: 0px;
  }

  a,
  a.active,
  a:active,
  a:focus,
  a:visited,
  a:hover {
    color: #545e98;
  }

  h1, h2, h3, h4, h5, h6 {
    font-family: 'Anton', sans-serif;
    font-weight: 400;
  }

  .app-head {
    padding: 60px 0 10px;
  }

  header {
    text-align: center;
  }

  hr {
    border: 0;
    height: 1px;
    background-image: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.30), rgba(0, 0, 0, 0));
    margin-bottom: 40px;
    margin-top: 40px;
  }

  #app {
    width: 100vw;
    height: 100%;
  }
</style>

<script>
import Map from './components/Map.vue'
import Feed from './components/LiveFeed.vue'
import Details from './components/Details.vue'
import L from 'leaflet'
import { setInterval } from 'timers';

export default {
  name: 'app',
  components: {
    Map,
    Feed,
    Details
  },

  data () {
    return {
      position: L.latLng(0, 0)
    }
  },
  methods: {
    getPOS () {
      setInterval(() => {
        fetch(process.env.VUE_APP_ISS_POSITION)
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
  }
}
</script>


