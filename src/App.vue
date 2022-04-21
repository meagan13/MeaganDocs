<template>
  <div>
    <Navigation></Navigation>
  </div>

  <!-- <div class="bg-red-300 py-3" id="nav">
      <router-link className="px-5 text-xl" :to="{ name: 'Home' }">Home</router-link>
      <router-link className="px-5 text-xl" to="/about">About</router-link>
      <router-link className="px-5 text-xl" to="/editor">Editor</router-link>
  </div> -->

  <!-- <router-view /> -->

</template>

<script>
  import Navigation from './components/Navigation.vue'

  export default {
    name: 'app',
    components: {
      'Navigation': Navigation
    },

  }
</script>
