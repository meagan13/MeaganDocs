<template>
  <div id="nav">
      <router-link className="px-5" :to="{ name: 'Home' }">Home</router-link>
      <router-link className="px-5" to="/about">About</router-link>
      <router-link className="px-5" to="/editor">Editor</router-link>
  </div>

  <router-view />

</template>
