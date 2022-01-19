<template>
    <div id="app">
        <Header @searchFilms="getFilms($event)" />
        <Main :films="films" />
    </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

import axios from 'axios';

export default {
    name: "App",
    components: {
        Header,
        Main,
    },
    data() {
        return {
            query: 'https://api.themoviedb.org/3/search/movie?api_key=524d95d10c0a6f36e2a3d1bd584407a5&language=it-IT&query=',
            films: []
        }
    },
    methods: {
        getFilms(value) {
            axios
                .get(`${this.query}${value}`)
                .then(result => {
                    this.films = result.data.results;
                })
                .catch(error => {
                    console.log(error);
                })
        }
    }
};
</script>

<style lang="scss">
@import "./assets/scss/partials/_commons.scss";
</style>
