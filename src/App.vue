<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <User></User>
  <!-- <botton class="button is-primary">Primary</botton> -->

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import User from './user/User'

import '../node_modules/bulma'

export default {
  name: 'App',
  components: {
    User
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
