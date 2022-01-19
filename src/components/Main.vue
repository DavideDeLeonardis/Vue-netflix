<template>
    <main>
        <Card
            v-for="(film, index) in films"
            :key="index"
            :title="film.title"
            :originalTitle="film.original_title"
            :lang="film.original_language"
            :vote="film.vote_average"
            :overview="film.overview"
        />
        <!-- :image="film.poster_path" -->
    </main>
</template>

<script>
import axios from 'axios';
import Card from './Card.vue'

export default {
    name: 'Main',
    components: {
        Card
    },
    props: {
        
    },
    data() {
        return {
            query: 'https://api.themoviedb.org/3/search/movie?api_key=524d95d10c0a6f36e2a3d1bd584407a5&language=it-IT',
            films: [],
            queryFinal: 'Ritorno'  // esempio inputText
            // queryFinal: ''
        }
    },
    computed: {
        
    },
    created() {
        axios.get(this.query, {
            params: {
                query: this.queryFinal
            }
        }).
        then(result => {
            this.films = result.data.results
        }).
        catch(error => {
            console.log(error);
        })
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_main.scss";
</style>
