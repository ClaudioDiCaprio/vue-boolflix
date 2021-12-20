<template>
  <div id="app">
   <Header @movieSearch="movieResult" @tvSearch="tvResult"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
export default {
  name: 'App',
  components: {
    Header,
  }
}
</script>

<style lang="scss">

 * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  #app {
    min-height: 200vh;
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    background-color: #141414;

  }
</style>
