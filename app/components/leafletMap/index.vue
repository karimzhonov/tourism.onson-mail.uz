<template>
  <div id="map_kadagentlik"></div>
</template>
<script>
import "leaflet/dist/leaflet.css"
import L from "leaflet"

export default {
  name: 'Map',
  components: {Location},
  data() {
    return {
      loading: true,
      map: null,
    }
  },
  async mounted() {
    this.loading = true
    this.loading = false
    setTimeout(this.init_map, 1000)
  },
  unmounted() {
    this.map.remove()
  },
  methods: {
    init_map() {
      const schema = L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png')
      this.map = L.map('map_kadagentlik', {
        center: [41.2808622, 65.2984895],
        zoom: 6,
        zoomControl: false,
        preferCanvas: true,
        layers: [schema],
      })
      this.map.attributionControl.setPrefix('')
    }
  }

}
</script>
<style>
#map_kadagentlik {
  width: 100%;
  height: 100vh;
  background-color: transparent;
  outline: none;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.dark #map_kadagentlik img {
  filter: invert(80%) hue-rotate(160deg) saturate(280%) brightness(85%) contrast(120%);
}
</style>