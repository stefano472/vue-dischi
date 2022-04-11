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
    
        <SpinnerLoader v-else />
      
  </main>
</template>

<script>
import axios from "axios";
import MusicCard from "./musicCard.vue";
import SpinnerLoader from "./SpinnerLoader.vue";


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
        MusicCard,
        SpinnerLoader
    }

}
</script>

<style scoped lang="scss">
main {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    .container {
        width: min(70%, 1200px);
        margin: auto;
        display: flex;
        gap: 1rem;
        flex-wrap: wrap;
    }
}
</style>