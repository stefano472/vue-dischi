<template>
    <select v-model="authorSelected" @change="showAuthorSelected" name="author-selection" id="author-selection">
        <option v-for="author in authorType" :key="author" :value="author" > 
            {{ author }} 
        </option>
    </select>
</template>

<script>
export default {
    name: 'SelectAuthor',
    data() {
        return {
            authorSelected: 'All',
        }
    },
    props: {
        authorType: Array
    }, 
    methods: {
        showAuthorSelected() {
            // this.authorSelected = getValue;
            console.log(this.authorSelected)
            this.$emit('searchByAuthor', this.authorSelected)
        }
    }
}
</script>

<style>

</style>