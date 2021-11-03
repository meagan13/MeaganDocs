<template>
  <div class="bg-green-800 p-3 text-xl w-screen" id="nav">
      <!-- <router-link className="px-5 text-gray-200" :to="{ name: 'Home' }">Home</router-link>
      <router-link className="px-5 text-gray-200" to="/about">About</router-link> -->
      <router-link className="px-5 text-gray-200" to="/editor">Datagrove Editor</router-link>
  </div>

  <router-view />

</template>

<script>
export default {
    name: 'Navigation',
    data() {
        return {
            links: [
                {
                    id: 0,
                    text: "Home",
                    page: "/"
                },
                {
                    id: 1,
                    text: "About",
                    page: "/about"
                },
                {
                    id: 2,
                    text: "Editor",
                    page: '/editor'
                }
            ]
        }
    }
}

</script>
