<template>
  <l-map style="height: 350px" :zoom="zoom" :center="center">
    <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    <l-marker v-for="fire, index in filtered" :key="index" :lat-lng="[fire.latitude, fire.longitude]" :icon="icon">
      <l-popup>
        Lat: {{ fire.latitude }}
        <br>
        Lon: {{ fire.longitude }}
        <br>
        Date: {{ fire.date }}
      </l-popup>
    </l-marker>
  </l-map>
</template>

<script>
import {LMap, LTileLayer, LMarker, LPopup} from 'vue2-leaflet'
import { icon } from "leaflet";

export default {
  name: "Map",
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup
  },
  props: {
    filtered: {
      type: Array
    }
  },
  data () {
    return {
      url: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
      attribution:
        '&copy; <a target="_blank" href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      zoom: 1,
      center: [44.417628, 8.886484], //Genova
      icon: icon({
        iconUrl: "https://cdn-icons-png.flaticon.com/512/426/426833.png",
        iconSize: [25, 25],
        iconAnchor: [16, 37]
      }),
    };
  },
  mounted() {
    console.log(this.$props.filtered);
  }
}
</script>
