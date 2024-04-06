<template>
  <section class="hero">
    <div class="hero-content">
      <h4>find your block</h4>
      <h1>Encontre os <span>melhores blocos</span> de carnaval de 2023</h1>
      <form class="hero-form" @submit.prevent.stop="search">
        <div class="form-group">
          <div class="form-control">
            <img src="../../images/search.svg" alt="" />
            <input
              type="text"
              name="title"
              id="title"
              class="input-control"
              placeholder="Pesquise por nome"
              v-model="title"
            />
          </div>
        </div>
        <div class="form-group has-icon">
          <div class="form-control">
            <img src="../../images/marker.svg" alt="" />
            <select name="state" id="state" class="input-control" v-model="state">
              <option value="" selected>Selecione um estado</option>
              <option value="BA">Bahia</option>
              <option value="PE">Pernambuco</option>
              <option value="RJ">Rio de Janeiro</option>
              <option value="SC">Santa Catarina</option>
              <option value="SP">São Paulo</option>
            </select>
          </div>
        </div>
        <button class="btn">Buscar agora</button>
      </form>
    </div>
  </section>
</template>
<script>
export default {
  data() {
    return {
      title: '',
      state: ''
    }
  },
  methods: {
    search() {
      let data = JSON.parse(JSON.stringify(this.title))
      data
        .normalize('NFD')
        .replace(/[\u0300-\u036f]/g, '')
        .toLowerCase()
      this.$emit('search', { title: data, state: this.state })
    }
  }
}
</script>