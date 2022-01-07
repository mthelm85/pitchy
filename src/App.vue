<template>
  <div id="app">
    <Pitch msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Pitch from './components/Pitch.vue'

export default {
  name: 'App',
  components: {
    Pitch
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
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}
</style>
