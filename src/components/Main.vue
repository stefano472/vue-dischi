<template>
  <main>
        <div v-if="musicAlbums.length > 0" class="container">
            <div class="selection">
                <!-- <select name="genre-selection" id="genre-selection">
                    <option v-for="genre in genreType" 
                    :key="genre" 
                    :value="genre"
                    > 
                        {{ genre }} 
                    </option>
                </select> -->
                <p> Select a genre</p>
                <SelectGenre :genreType="genreType" @searchByGenre="filterByGenre" />
            </div>
            <div class="card-container">
                <MusicCard v-for="album in filteredArray" :key="album.poster" 
                    :img="album.poster" 
                    :genre="album.genre" 
                    :title="album.title" 
                    :author="album.author" 
                    :year="album.year"
                /> 
            </div>
        </div>
    
        <SpinnerLoader v-else />
      
  </main>
</template>

<script>
import axios from "axios";
import MusicCard from "./musicCard.vue";
import SpinnerLoader from "./SpinnerLoader.vue";
import SelectGenre from "./SelectGenre.vue";

export default {
    name: "MainComponent",
    data() {
        return {
            musicAlbums: [], 
            genreType: [],
            myGenre: ''
        }
    },
    props: {
        library: String
    },
    mounted() {
        this.getElementArray()
        // console.log(this.myGenre)
    }, 
    computed: {
        filteredArray() {
            if (this.myGenre.length===0 || this.myGenre === 'All') {
                return this.musicAlbums
            }
            return this.musicAlbums.filter( card => {
                console.log(this.myGenre)
                console.log('mygenre', card.genre);
                // card.genre.includes(this.myGenre)
                return card.genre.includes(this.myGenre)
            })
        }
    },
    methods: {
        getElementArray() {
            axios.get(this.library)
                .then(response => {
                    if (response.data.success) {
                        this.musicAlbums = response.data.response;
                        this.genreType.push('All')
                        const genre = response.data.response.map((item) => item.genre);
                        genre.forEach(element => {
                            if (!this.genreType.includes(element)) {
                                this.genreType.push(element)
                            }
                        });
                    } 
                }
            )
        },
        filterByGenre(genre) {
            this.myGenre= genre
        }
    },
    components: {    
        MusicCard,
        SpinnerLoader, 
        SelectGenre
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
        width: min(80%, 1200px);
        margin: auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 2rem;
        .selection {
            display: flex;
            gap: 1rem;
            color: white;
        }
        .card-container {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            justify-content: center;
        }
    }
}
</style>