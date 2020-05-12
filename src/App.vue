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
  /*font-family: Avenir, Helvetica, Arial, sans-serif;*/
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /*margin-top: 15%;*/
  position: absolute;
  height: 100%;
  width: 100%;
  /*background-color: black;*/
}
</style>
