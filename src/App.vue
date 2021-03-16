<template>
  <div id="app">
    <Order/>
  </div>
</template>

<script>
import Order from './components/Order.vue'

export default {
  name: 'App',
  components: {
    Order
  }
}
</script>

<style>
#app {
  background-color: greenyellow;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%
}
</style>
