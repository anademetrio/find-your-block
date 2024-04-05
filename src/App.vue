<template>
  <section class="hero">
    <div class="hero-content">
      <h4>find your block</h4>
      <h1>Encontre os <span>melhores blocos</span> de carnaval de 2023</h1>
      <div class="hero-form">
        <div class="form-group">
          <div class="form-control">
            <img src="../images/search.svg" alt="" />
            <input
              type="text"
              name="title"
              id="title"
              class="input-control"
              placeholder="Pesquise por nome"
            />
          </div>
        </div>
        <div class="form-group has-icon">
          <div class="form-control">
            <img src="../images/marker.svg" alt="" />
            <select name="city" id="city" class="input-control">
              <option value="" selected disabled>Selecione um estado</option>
              <option value="BA">Bahia</option>
              <option value="PE">Pernambuco</option>
              <option value="RJ">Rio de Janeiro</option>
              <option value="SC">Santa Catarina</option>
              <option value="SP">São Paulo</option>
            </select>
          </div>
        </div>
        <button class="btn">Buscar agora</button>
      </div>
    </div>
  </section>
  <section class="cards">
    <div class="d-flex">
      <div class="subtitle">Blocos recomendados</div>
      <div class="btn-group">
        <button class="btn sm" :class="view === 'map' ? 'text' : ''" @click="changeView('list')">
          lista
        </button>
        <button class="btn sm" :class="view === 'list' ? 'text' : ''" @click="changeView('map')">
          mapa
        </button>
      </div>
    </div>
    <div class="grid-cards" v-show="view === 'list'">
      <div class="card" v-for="role in roles" :key="role.image">
        <div class="card-image">
          <img :src="`../images/${role.image}.jpg`" :alt="role.title" />
        </div>
        <div class="card-body">
          <div class="card-title">{{ role.title }}</div>
          <div class="card-desc">
            Amet minim mollit non deserunt ullamco est sit aliqua dolor do amet sint.
          </div>
        </div>
        <div class="card-footer">
          <img src="../images/marker.svg" alt="" />
          <div>{{ role.local }}, {{ role.state }}</div>
        </div>
      </div>
    </div>
    <div id="mapContainer" class="map" v-show="view === 'map'"></div>
  </section>
  <footer>Copyright©. Todos Direitos Reservados.</footer>
</template>
<script>
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'
import roles from './data/roles'
export default {
  data() {
    return {
      roles,
      view: 'map',
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
    this.view = 'list'
  },
  onBeforeUnmount() {
    if (this.map) {
      this.map.remove()
    }
  },
  methods: {
    changeView(view) {
      this.view = view
    }
  }
}
</script>
