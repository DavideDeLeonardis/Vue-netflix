<template>
    <div id="app">
        <Header @searchCards="search($event)" />
        <Main :cards="cards" />
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
            
            query: 'https://api.themoviedb.org/3/search/',
            api_key: '524d95d10c0a6f36e2a3d1bd584407a5',
            language: 'it-IT',
            inputText: '',
            cards: {
                films: [],
                series: []
            }
        }
    },
    methods: {
        search(value) {
            this.inputText = value;
            if (value != '') {
                this.getFilms();
                this.getSeries();
            } else {
                this.cards.films = [];
                this.cards.series = [];
            }
        },
        getFilms() {
            axios
                .get(`${this.query}${'movie'}`, { 
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                        query: this.inputText
                    }
                })
                .then(result => {
                    this.cards.films = result.data.results;
                })
                .catch(error => {
                    console.log(error);
                })
        },
        getSeries() {
            axios
                .get(`${this.query}${'tv'}`, { 
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                        query: this.inputText
                    }
                })
                .then(result => {
                    this.cards.series = result.data.results;
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
