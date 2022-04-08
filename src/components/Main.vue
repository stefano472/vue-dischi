<template>
  <main>
      <div v-if="musicAlbums.length > 0" class="container">
        <MusicCard v-for="album in musicAlbums" :key="album.poster" 
            :img="album.poster" 
            :genre="album.genre" 
            :title="album.title" 
            :author="album.author" 
            :year="album.year"
        /> 
      </div>
  </main>
</template>

<script>
import axios from "axios";
import MusicCard from "./musicCard.vue";

export default {
    name: "MainComponent",
    data() {
        return {
            musicAlbums: []
        }
    },
    props: {
        library: String
    },
    mounted() {
        this.getElementArray()
    }, 
    methods: {
        getElementArray() {
            axios.get(this.library)
                .then(response => {
                    if (response.data.success) {
                        this.musicAlbums = response.data.response
                    }
                }
            )
        }
    },
    components: {    
        MusicCard
    }

}
</script>

<style scoped lang="scss">
main {
    margin-top: 4rem;
    .container {
        width: min(80%, 1200px);
        margin: auto;
        padding: 3rem 0;
        display: flex;
        gap: 1rem;
        flex-wrap: wrap;
    }
}
</style>