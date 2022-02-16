<template>
  <div class="bg-green-100 font-mono text-2xl lg:text-4xl h-full w-screen flex items-center" id="nav">
      <!-- <router-link className="px-5 text-gray-200" :to="{ name: 'Home' }">Home</router-link>
      <router-link className="px-5 text-gray-200" to="/about">About</router-link> -->
      <div class="flex h-full w-1/6 content-center items-center justify-center">
        <a href="/"><img class="h-20 w-20 lg:h-32 lg:w-32" src="../../images/datagrove_logo_shadow.png" alt="datagrove logo"></a>
      </div>

      <div class="flex h-full w-5/6 content-center items-center justify-start">
        <router-link to="/editor">
            Text Editor
        </router-link>
      </div>
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
    },
}

</script>
