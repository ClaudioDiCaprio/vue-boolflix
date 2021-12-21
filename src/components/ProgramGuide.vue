<template>
    <main>
        <Movie v-for="movie, i in movieResult" :key="'movie' + i" :movie="movie"/>
    </main>
</template>

<script>
import Movie from '@/components/Movie.vue'
export default {
    name: 'ProgramGuide',
    components: {
        Movie,
       
    },
    props: {
        movieRes: Array,
    },
    computed: {
        movieResult() {
            return this.movieRes
        },
    }
}
</script>

<style lang="scss" scoped>
    main {
        width: 90%;
        margin: 0 auto;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        min-height: calc(100vh - 100px);
    }