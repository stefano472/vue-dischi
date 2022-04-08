<template>
  <div id="app">
    <Header />
    <Main :library="apiURL"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Main from './components/Main.vue'

export default {
  name: 'App',
  data() {
    return {
      apiURL: 'https://flynn.boolean.careers/exercises/api/array/music'
    }
  },
  components: {
    Header,
    Main
  }
}
</script>

<style lang="scss">
@import "~@fontsource/raleway/index.css";
@import "~@fontsource/raleway/700.css";


* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: 'raleway', sans-serif;
}
body {
  background: #1e2d3b;
  width: 100%;
  height: 100vh;
}
#app {
  padding: 4.5rem 0 0.5rem;
  height: 100%;
  display: flex;
  align-items: center;
}
</style>
