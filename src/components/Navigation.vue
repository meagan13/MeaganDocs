<template>
  <div class="bg-red-300 p-3 text-xl w-screen" id="nav">
      <router-link className="px-5" :to="{ name: 'Home' }">Home</router-link>
      <router-link className="px-5" to="/about">About</router-link>
      <router-link className="px-5" to="/editor">Editor</router-link>
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
