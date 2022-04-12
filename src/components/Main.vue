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
                <p> Select genre</p>
                <SelectGenre :genreType="genreTypeArray" @searchByGenre="filterByGenre" />
                <p> Select author</p>
                <SelectAuthor :authorType="authorsArray" @searchByAuthor="filterByAuthor" />
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
import SelectAuthor from "./SelectAuthor.vue";

export default {
    name: "MainComponent",
    data() {
        return {
            musicAlbums: [], 
            // genreType: [],
            myGenre: '',
            myAuthor: ''
        }
    },
    props: {
        library: String
    },
    // in questo caso avrei potuto usare anche created() per generare l'array è un hooked method che viene eseguito una volta sola 
    // come mounted un attimo prima della creazione del DOM, quindi con created non posso avere accesso ad un elemento dellHTML con mounted sì
    mounted() {
        this.getElementArray()
        // console.log(this.myGenre)
    }, 
    computed: {
        filteredArray() {
            const arrayFiltrato = (this.myGenre==='' || this.myGenre === 'All') 
                    ? this.musicAlbums 
                    : this.musicAlbums.filter( card => card.genre.includes(this.myGenre))
            
            if (this.myAuthor === "All") {
                return arrayFiltrato;
            }
            return arrayFiltrato.filter((item) => item.author.includes(this.myAuthor))

            /*
            if (this.myGenre==='' || this.myGenre === 'All') {
                return this.musicAlbums
            }
            return this.musicAlbums.filter( card => {
                // console.log(this.myGenre)
                // console.log('mygenre', card.genre);
                return card.genre.includes(this.myGenre)
            })
            */
        },
        genreTypeArray() {
            const genres = ['All'];
            this.musicAlbums.map(item => item.genre).forEach(element => {
                        if (!genres.includes(element)) {
                            genres.push(element)
                        }});
            return genres
        },
        authorsArray() {
            const authors = ['All'];
            this.musicAlbums.map(item => item.author).forEach(element => {
                        if (!authors.includes(element)) {
                            authors.push(element)
                        }});
            return authors
        },
    },
    methods: {
        getElementArray() {
            axios.get(this.library).then(response => {
                if (response.data.success) {
                    this.musicAlbums = response.data.response;
                    /* metodo poco pratico perchè se dovessi cambiare l'array in modo dinamico dovrei cambiare manualmente l'array
                    this.genreType.push('All')
                    const genre = response.data.response.map((item) => item.genre);
                    genre.forEach(element => {
                        if (!this.genreType.includes(element)) {
                            this.genreType.push(element)
                        }
                    }) */
                    } 
                }
                // catch serve per prendere quei risultati qualora il then non venga eseguito(quindi faccio stampare in console un errore in tal caso)
            ).catch(error => console.log(error))
        },
        filterByGenre(genre) {
            this.myGenre= genre
        },
        filterByAuthor(author) {
            this.myAuthor= author
        }
    },
    components: {    
        MusicCard,
        SpinnerLoader, 
        SelectGenre,
        SelectAuthor
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
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 2rem;
        .selection {
            display: flex;
            align-items: center;
            gap: 1rem;
            color: white;
            p {
                font-size: 0.9rem;
            }
            select {
                background: #2e3a46;
                color: white;
                border-radius: 3px;
                padding: 0.2rem 0
            }
        }
        .card-container {
            width: 100%;
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
            justify-content: center;
        }
    }
}
</style>