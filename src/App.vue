<template>
  <Hero @search="search"></Hero>
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
    <List :roles="roles" v-show="view === 'list'"></List>
    <Map :roles="roles" v-show="view === 'map'"></Map>
  </section>
  <footer>Copyright©. Todos Direitos Reservados.</footer>
</template>
<script>
// @ts-ignore
import Hero from '@/components/Hero.vue'
// @ts-ignore
import List from '@/components/List.vue'
// @ts-ignore
import Map from '@/components/Map.vue'
import roles from '@/data/roles'
export default {
  components: {
    Hero,
    List,
    Map
  },
  data() {
    return {
      roles,
      view: 'map'
    }
  },
  mounted() {
    this.view = 'list'
  },
  methods: {
    changeView(view) {
      this.view = view
    },
    search({ title, state }) {
      let data = JSON.parse(JSON.stringify(roles))
      data = data.filter((e) => {
        const role_title = e.title
          .normalize('NFD')
          .replace(/[\u0300-\u036f]/g, '')
          .toLowerCase()
        if (state) {
          return role_title.includes(title) && e.state == state
        } else if (title) {
          return role_title.includes(title)
        } else {
          return data
        }
      })
      this.roles = data
    }
  }
}
</script>
