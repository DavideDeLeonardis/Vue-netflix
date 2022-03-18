<template>
    <div id="app">
        <Header
            @search="search($event)" 
            :genres="genresList"
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

export default {
    name: "App",
    components: {
        Header,
        Main
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
            apiStart: 'https://api.themoviedb.org/3/',   // Docs: https://developers.themoviedb.org/3/
            api_key: '524d95d10c0a6f36e2a3d1bd584407a5',
            language: 'it-IT',
            inputText: '',
        }
    },
    methods: {
        search(value) {
            this.inputText = value;
            if (value != '') {
                // Call to all movies and series only when input:text in not empty
                this.getSearched('search/movie', this.inputText, 'allFilms');
                this.getSearched('search/tv', this.inputText, 'allSeries');
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
                    // For each case, object this.all and object this.populars are filled
                    switch (array) {
                        case 'allFilms':
                            this.all.films = result.data.results;
                            break;
                        case 'allSeries':
                            this.all.series = result.data.results;
                            break;
                        case 'filmsPopular':
                            this.populars.films = result.data.results.slice(0, 12); // Paginate only 12 cards per array
                            break;
                        case 'seriesPopular':
                            this.populars.series = result.data.results.slice(0, 12); // Paginate only 12 cards per array
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

        // Get movies and series' generes
        this.getGenres('movie', 'films');
        this.getGenres('tv', 'series');

        // Get trending movies and series in current day
        this.getSearched('trending/movie/day', '', 'filmsPopular');
        this.getSearched('trending/tv/day', '', 'seriesPopular');
    }
};
</script>

<style lang="scss">
@import "./assets/scss/_commons.scss";

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
