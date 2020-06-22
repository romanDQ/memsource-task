<template>
  <div id="app">   
    <dashBoard/>
  </div>
</template>

<script>
import dashBoard from './components/dashBoard'

export default {
  name: 'App',
  components: {
  dashBoard,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
