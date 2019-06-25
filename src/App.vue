<template>
  <div id="app">
    <ShutterSlider interval="3000"/>
  </div>
</template>

<script>
import ShutterSlider from './components/ShutterSlider.vue'

export default {
  name: 'app',
  components: {
    ShutterSlider
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
