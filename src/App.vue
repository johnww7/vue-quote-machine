<template>
  <div id="app">
    <QuoteMachine quoteMessage="Welcome to Your Vue.js App"
    quotesAuthor="John okay"/>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
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
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 15%;
  
}
</style>
