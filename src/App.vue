<template>
    <div id="app">
        <Header
            @search="search($event)" 
        />
        <Main
            v-if="ready"
            :inputText="inputText"
            :cards="cards"
            :populars="populars"
        />
        <div v-else class="else">
            Boolflix is loading...<br>
            <font-awesome-icon
                icon="circle-notch"
            />
        </div>
    </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

import axios from 'axios';

import { library } from '@fortawesome/fontawesome-svg-core';
import { faCircleNotch } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
library.add(faCircleNotch);

export default {
    name: "App",
    components: {
        Header,
        Main,
        FontAwesomeIcon
    },
    data() {
        return {
            ready: false,
            cards: {
                films: null,
                series: null
            },
            populars: {
                films: [],
                series: []
            },
            genresList: {
                films: null,
                series: null
            },
            apiStart: 'https://api.themoviedb.org/3/',
            api_key: '524d95d10c0a6f36e2a3d1bd584407a5',
            language: 'it-IT',
            inputText: '',
            selectValue: ''
        }
    },
    methods: {
        search(value) {
            this.inputText = value;
            if (value != '') {
                this.getSearched('search/movie', this.inputText, 'filmsSearched');
                this.getSearched('search/tv', this.inputText, 'seriesSearched');
            } else {
                this.cards.films = null;
                this.cards.series = null;
            }
        },
        getSearched(endPoint, query, array) {
            axios
                .get(`${this.apiStart}${endPoint}`, { 
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                        query: query
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
                        case 'seriesPopular':
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
        // Load page
        setTimeout(() => {
            this.ready = true
        }, 1000);

        this.getSearched('trending/movie/day', '', 'filmsPopular');
        this.getSearched('trending/tv/day', '', 'seriesPopular');
    }
};
</script>

<style lang="scss">
@import "./assets/scss/partials/_commons.scss";

.else {
        font-size: 2em;
        text-align: center;
        color: rgb(255, 255, 255);
        margin: 1em;
        
        .fa-circle-notch {
            font-size: 1.5em;
            margin-top: 20px;
            animation: spin 1s linear infinite;
            
            @keyframes spin {
                from {
                    transform: rotate(0);
                }
                to {
                    transform: rotate(360deg);
                }
            }
        }
    }
</style>
