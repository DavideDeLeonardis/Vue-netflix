<template>
    <div id="app">
        <Header @search="search($event)" />
        <Main 
            :inputText="inputText"
            :cards="cards"
            :populars="populars"
        />
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
            query: 'https://api.themoviedb.org/3/',
            api_key: '524d95d10c0a6f36e2a3d1bd584407a5',
            language: 'it-IT',
            inputText: '',
            cards: {
                films: null,
                series: null
            },
            populars: {
                films: [],
                series: []
            }
        }
    },
    methods: {
        search(value) {
            this.inputText = value;
            if (value != '') {
                this.getSearched('search/movie', 'filmsSearched');
                this.getSearched('search/tv', 'seriesSearched');
            } else {
                this.cards.films = null;
                this.cards.series = null;
            }
        },
        getSearched(endPoint, array) {
            axios
                .get(`${this.query}${endPoint}`, { 
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                        query: this.inputText
                    }
                })
                .then(result => {
                    switch (array) {
                        case 'filmsSearched':
                            this.cards.films = result.data.results;
                            break;
                        case 'seriesSearched':
                            this.cards.series = result.data.results;
                            break;
                        case 'filmsPopular':
                            this.populars.films = result.data.results.slice(0, 8);
                            break;
                        default:
                            this.populars.series = result.data.results.slice(0, 8);
                            break;
                    }
                })
                .catch(error => {
                    console.log(error);
                })
        }
    },
    created() {
        this.getSearched('trending/movie/day', 'filmsPopular');
        this.getSearched('trending/tv/day', 'seriesPopular');
    }
};
</script>

<style lang="scss">
@import "./assets/scss/partials/_commons.scss";
</style>
