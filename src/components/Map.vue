<template>
  <div>
    <l-map
      :zoom="zoom"
      :center="position"
      :options="mapOptions"
      style="height:85vh;"
    >
      <l-tile-layer :url="url" :attribution="attribution" />
      <l-marker :lat-lng="position" :icon="icon" />
    </l-map>
  </div>
</template>

<style>
  @import "../../node_modules/leaflet/dist/leaflet.css";
</style>

<script>
import L from 'leaflet'
import { LMap, LTileLayer, LMarker } from 'vue2-leaflet'

export default {
  name: 'issmap',
  components: {
    LMap,
    LTileLayer,
    LMarker
  },
  data () {
    return {
      zoom: 4.5,
      url:'https://server.arcgisonline.com/ArcGIS/rest/services/NatGeo_World_Map/MapServer/tile/{z}/{y}/{x}',
      attribution:'Tiles &copy; Esri &mdash; National Geographic, Esri, DeLorme, NAVTEQ, UNEP-WCMC, USGS, NASA, ESA, METI, NRCAN, GEBCO, NOAA, iPC',
      mapOptions: {
        zoomSnap: 0.5,
        scrollWheelZoom: false
      },
      icon: L.icon({
        iconUrl: `${process.env.VUE_APP_SUB_FOLDER}static/international_space_station.svg`,
        iconSize: [64, 38],
        iconAnchor: [32, 19]
      })
    }
  },
  props: ['position']
}
</script>