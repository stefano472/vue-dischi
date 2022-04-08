<template>
  <div class="card">
      <img :src="img" :alt="title">
      <div class="info">
        <h2> {{title}} </h2>
        <p> {{author}} </p>
        <p> {{year}} </p>
      </div>
      <div> {{genre}} </div>
  </div>
</template>

<script>

/*
author: "Bon Jovi"
genre: "Rock"
poster: "https://www.onstageweb.com/wp-content/uploads/2018/09/bon-jovi-new-jersey.jpg"
title: "New Jersey"
year: "1988"
*/

export default {
    name: "MusicCard",
    props: {
        img: String,
        genre: String,
        title: String,
        author: String,
        year: String
    }

}
</script>

<style scoped lang="scss">
.card {
    flex-basis: calc(100% / 5 - 1rem * 4 / 5);
    padding: 1rem;
    background: #2e3a46;
    word-break: break-word;
}
img {
    aspect-ratio: 1/1;
    object-fit: cover;
    width: 100%;
}
h2 {
    padding: 0.5rem 0;
    font-weight: 700;
    text-transform: uppercase;
    font-size: 1.3rem;
    color: white;
    text-align: center;
}
</style>