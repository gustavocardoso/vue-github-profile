<template>
  <div id="app">
    <img src="./assets/logo.png" class="logo">
    <h1>Vue Github Profile</h1>
    <search-profile></search-profile>
  </div>
</template>

<script>
  import searchProfile from './components/SearchProfile.vue'

  export default {
    name: 'app',

    components: {
      searchProfile
    },

    data () {
      return {
      }
    }
  }
</script>

<style>
  body {
    font: normal normal 16px/1.5 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    overflow-x: hidden;
  }

  #app {
    width: 90%;
    text-align: center;
    color: #2c3e50;
    margin: 0 auto;
    padding: 2em 2em 0 2em;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0;
  }

  a {
    color: #42b983;
  }

  .logo {
    width: 80px;
  }
</style>
