<template>
    <select @change="showGenreSelected($event)" name="genre-selection" id="genre-selection">
        <option v-for="genre in genreType" :key="genre" :value="genre" > 
            {{ genre }} 
        </option>
    </select>
</template>

<script>
export default {
    name: 'SelectGenre',
    data() {
        return {
            genreSelected: ''
        }
    },
    props: {
        genreType: Array
    }, 
    methods: {
        showGenreSelected(event) {
            this.genreSelected = event.target.value,
            this.$emit('searchByGenre', this.genreSelected)
        }
    }
}
</script>

<style>

</style>