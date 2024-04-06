<template>
  <div class="grid-cards">
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
        <img src="../../images/marker.svg" alt="" />
        <div>{{ role.local }}, {{ role.state }}</div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: ['roles']
}
</script>