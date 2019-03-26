<template>
  <l-map
    :zoom="zoom"
    :center="position"
    :options="mapOptions"
  >
    <l-tile-layer :url="url" :attribution="attribution" />
    <l-marker :lat-lng="position" :icon="icon" />
    <l-circle :lat-lng="position" :radius="radius" />
  </l-map>
</template>

<style>
  @import "../../node_modules/leaflet/dist/leaflet.css";

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    width: 100vw;
    height: 85vh;
  }
</style>

<script>
import L from 'leaflet'
import { LMap, LTileLayer, LMarker, LCircle } from 'vue2-leaflet'

export default {
  name: 'issmap',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LCircle
  },
  data () {
    return {
      zoom: 4.5,
      url:'https://server.arcgisonline.com/ArcGIS/rest/services/NatGeo_World_Map/MapServer/tile/{z}/{y}/{x}',
      attribution:'Tiles &copy; Esri &mdash; National Geographic, Esri, DeLorme, NAVTEQ, UNEP-WCMC, USGS, NASA, ESA, METI, NRCAN, GEBCO, NOAA, iPC',
      mapOptions: {
        zoomSnap: 0.5
      },
      icon: L.icon({
        iconUrl: '/static/international_space_station.svg',
        iconSize: [64, 38],
        iconAnchor: [32, 19]
      }),
      radius: 1500e3
    }
  },
  props: ['position']
}
</script>