<template>
  <div id="app">
    <Info @close="hide=!hide" v-show="!hide" />
    <Pitch @close="hide=!hide" msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Info from './components/Info.vue'
import Pitch from './components/Pitch.vue'

export default {
  name: 'App',
  components: {
    Info,
    Pitch
  },
  data () {
    return {
      hide: false
    }
  },
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
  height: 98vh;
}
</style>
