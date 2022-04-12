<template>
  <div class="card">
      <img :src="img" :alt="title">
      <div class="info">
        <h2> {{title}} </h2>
        <p class="author"> {{author}} </p>
        <p class="year"> {{year}} </p>
      </div>
      <div class="genre"> {{genre}} </div>
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
    padding: 0.5rem;
    border-radius: 5px;
    background: #2e3a46;
    word-break: break-word;
    position: relative;
    display: flex;
    flex-direction: column;
}
img {
    aspect-ratio: 1/1;
    object-fit: cover;
    width: 100%;
    border-radius: 5px;
}
.info {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    h2 {
        flex-grow: 1;
        padding: 0.5rem 0;
        font-weight: 700;
        text-transform: uppercase;
        font-size: 1.2rem;
        color: white;
        text-align: center;
    }
    .author {
        color: #767879;
        font-size: 0.9rem;
    }
    .year {
        color: #767879;
    }
    
}
.genre {
    position: absolute;
    bottom: 0.5rem;
    right: 0.5rem;
    color: white;
    font-size: 0.7rem;
}
</style>