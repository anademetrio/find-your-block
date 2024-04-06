<template>
  <div id="mapContainer" class="map"></div>
</template>
<script>
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'
export default {
  props: ['roles'],
  data() {
    return {
      map: null
    }
  },
  mounted() {
    this.map = L.map('mapContainer').setView([-10.3333333, -53.2], 5)
    L.tileLayer('http://{s}.tile.osm.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(this.map)

    let markers = []
    this.roles.forEach((role, i) => {
      markers[i] = L.marker([role.lat, role.long]).addTo(this.map)
      markers[i]
        .bindPopup(
          `<div class="popup">
            <img src="../images/${role.image}.jpg" />
            <div>
              <b>${role.title}</b><br>
              ${role.local}, ${role.state}
            </div>
          </div>`
        )
        .openPopup()
    })
  },
  onBeforeUnmount() {
    if (this.map) {
      this.map.remove()
    }
  }
}
</script>