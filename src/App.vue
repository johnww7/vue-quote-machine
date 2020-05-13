<template>
  <div id="app">
    <QuoteMachine/>
  </div>
</template>

<script>

import QuoteMachine from './components/QuoteMachine.vue'

export default {
  name: 'App',
  components: {
    QuoteMachine
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: absolute;
  height: 100%;
  width: 100%;
}
</style>
