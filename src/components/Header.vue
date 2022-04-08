<template>
  <header>
      <img src="../../public/spotify-logo.png" alt="logo">
  </header>
</template>

<script>
export default {
    name: "HeaderComponent"

}
</script>

<style scoped lang="scss">
header {
    position: fixed;
    height: 4rem;
    padding: 0.5rem 1.5rem;
    width: 100%;
    background: #2e3a46;
    img {
        height: 100%;
    }
}
</style>