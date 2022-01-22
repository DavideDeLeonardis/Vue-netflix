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
                this.getSearched('search/movie', 'films');
                this.getSearched('search/tv', 'series');
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
                    if (array == 'films') {
                        this.cards.films = result.data.results;
                    } else {
                        this.cards.series = result.data.results;
                    }
                })
                .catch(error => {
                    console.log(error);
                })
        },
        getTrending(endPoint, array) {
            axios
                .get(`${this.query}${endPoint}`, { 
                    params: {
                        api_key: this.api_key
                    }
                })
                .then(result => {
                    if (array == 'films') {
                        this.populars.films = result.data.results.slice(0, 9)
                    } else {
                        this.populars.series = result.data.results.slice(0, 9)
                    }
                })
                .catch(error => {
                    console.log(error);
                })
        }
    },
    created() {
        this.getTrending('trending/movie/day', 'films');
        this.getTrending('trending/tv/day', 'series');
    }
};
</script>

<style lang="scss">
@import "./assets/scss/partials/_commons.scss";
</style>
