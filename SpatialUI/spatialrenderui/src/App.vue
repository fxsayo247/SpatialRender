<template>
  <main class="app-layout">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <LandingStrip/>
    <Upload/>
    <PromptInput/>
  </main>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

import LandingStrip from './components/landing/LandingStrip.vue'
import Upload from './components/landing/Upload.vue'
import PromptInput from './components/landing/PromptInput.vue'



export default {
  name: 'App',
  components: {
    // HelloWorld,
    LandingStrip,
    Upload,
    PromptInput
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.app-layout {
  display: flex;
  flex-direction: column;
  gap: 1.5rem; /* Adds some space between your components */
}
</style>
