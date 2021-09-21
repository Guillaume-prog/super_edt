<template>
  <v-app>
    <Navbar />

    <div id="main">
      <Home />
    </div>
  </v-app>
</template>

<style>
  @import url('https://fonts.googleapis.com/css2?family=B612+Mono&display=swap');
</style>

<script>
import Navbar from '@/components/Navbar.vue'
import Home from '@/vues/Home.vue'

export default {
  name: 'App',

  components: {
    Navbar,
    Home
  },

  data: () => ({
    events: {}
  }),
};
</script>
