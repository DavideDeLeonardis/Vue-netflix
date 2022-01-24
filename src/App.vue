<template>
    <div id="app">
        <Header
            :genres="genresList"
            @search="search($event)" 
        />
        <Main
            v-if="showMainVar"
            :inputText="inputText"
            :all="all"
            :populars="populars"
        />
        <div v-else class="elseApp">
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
            showMainVar: false,
            all: {
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
                this.all.films = null;
                this.all.series = null;
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
                            this.all.films = result.data.results;
                            this.getGenres('movie', 'films');
                            break;
                        case 'seriesSearched':
                            this.all.series = result.data.results;
                            this.getGenres('tv', 'series');
                            break;
                        case 'filmsPopular':
                            this.populars.films = result.data.results.slice(0, 8);
                            this.getGenres('movie', 'films');
                            break;
                        case 'seriesPopular':
                            this.populars.series = result.data.results.slice(0, 8);
                            this.getGenres('tv', 'series');
                            break;
                    }
                })
                .catch(error => {
                    console.log(error);
                })
        },
        getGenres(endPointType, array) {
            axios
                .get(`${this.apiStart}genre/${endPointType}/list`, { 
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                    }
                })
                .then(result => {
                    switch (array) {
                        case 'films':
                            this.genresList.films = result.data.genres;
                            break;
                        case 'series':
                            this.genresList.series = result.data.genres;
                            break;
                    }
                })
                .catch(error => {
                    console.log(error);
                })
        }
    },
    created() {
        // Loading page
        setTimeout(() => {
            this.showMainVar = true
        }, 1000);
        
        console.log(this.genresList);

        this.getSearched('trending/movie/day', '', 'filmsPopular');
        this.getSearched('trending/tv/day', '', 'seriesPopular');
    }
};
</script>

<style lang="scss">
@import "./assets/scss/partials/_commons.scss";

.elseApp {
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
