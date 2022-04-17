<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <ScoringPage />
  </div>
</template>

<script>
import ScoringPage from './components/ScoringPage.vue'

export default {
  name: 'App',
  components: {
    ScoringPage
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
