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
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  background: #1e2d3b;
  width: 100%;
  height: 100vh;
}
</style>
