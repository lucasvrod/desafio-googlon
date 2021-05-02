<template>
  <div id="app">
    <Googlon msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import Googlon from './components/Googlon.vue'

export default {
  name: 'App',
  components: {
    Googlon
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
</style>
