<template>
  <p v-if="$fetchState.pending">Fetching mountains...</p>
  <p v-else-if="$fetchState.error">An error occurred :(</p>
  <div v-else>
    <h1>Nuxt Mountains</h1>
    <ul class="mountains__list">
      <li class="mountains__item" v-for="mountain of mountains" :key="mountain.title">{{ mountain.title }}</li>
    </ul>
    <button @click="$fetch">Refresh</button>
  </div>
</template>

<script>
export default {
  data () {
    return {
      mountains: []
    }
  },
  async fetch () {
    this.mountains = await fetch(
      'https://api.nuxtjs.dev/mountains'
    ).then(res => res.json())
  }
}
</script>

<style scoped>
.mountains__list {
  margin: 0;
  padding: 0;
  list-style: none;
}
</style>
