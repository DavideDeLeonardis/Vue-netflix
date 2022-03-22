<template>
    <div id="app">
        <Header
            :genres="genresList"
            @emitSelectFilm="selectGenreFilms($event)"
            @emitSelectSerie="selectGenreSeries($event)"
            @search="search($event)"
        />

        <Main
            v-if="showMainVar"
            :inputText="inputText"
            :all="allFiltered"
            :populars="popularsFiltered"
        />

        <div v-else class="elseApp">
            Boolflix is loading...<br />
            <font-awesome-icon icon="circle-notch" />
        </div>
    </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

import axios from "axios";

export default {
    name: "App",
    components: {
        Header,
        Main,
    },
    data() {
        return {
            apiStart: "https://api.themoviedb.org/3/", // Docs: https://developers.themoviedb.org/3/
            api_key: "524d95d10c0a6f36e2a3d1bd584407a5",
            language: "it-IT",
            showMainVar: false,
            all: {
                films: [],
                series: [],
            },
            allFiltered: {
                films: [],
                series: [],
            },
            populars: {
                films: [],
                series: [],
            },
            popularsFiltered: {
                films: [],
                series: [],
            },
            genresList: { // two different genres list from api!
                films: null,
                series: null,
            },
            inputText: "",
            valueSelectFilm: "tutti",
            valueSelectSerie: "tutte",
        };
    },
    methods: {
        getGenres(endPointType, array) {
            axios
                .get(`${this.apiStart}genre/${endPointType}/list`, {
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                    },
                })
                .then((result) => {
                    switch (array) {
                        // Push genres in array genresList.films and genresList.series
                        case "films":
                            this.genresList.films = result.data.genres;
                            break;
                        case "series":
                            this.genresList.series = result.data.genres;
                            break;
                    }
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        selectGenreFilms(valueSelectFilm) {
            this.valueSelectFilm = valueSelectFilm;
            if (this.valueSelectFilm === "tutti") {
                // Display allFiltered and popularsFiltered films
                this.allFiltered.films = this.all.films;
                this.popularsFiltered.films = this.populars.films;
            } else {
                // Filter films with genre_id == valueSelectFilm
                this.allFiltered.films = this.all.films.filter(film => {
                    return film.genre_ids.includes(this.valueSelectFilm);
                });
                this.popularsFiltered.films = this.populars.films.filter(film => {
                    return film.genre_ids.includes(this.valueSelectFilm);
                });
            }
        },
        selectGenreSeries(valueSelectSerie) {
            this.valueSelectSerie = valueSelectSerie;
            if (this.valueSelectSerie === "tutte") {
                // Display allFiltered and popularsFiltered series
                this.allFiltered.series = this.all.series;
                this.popularsFiltered.series = this.populars.series;
            } else {
                // Filter series with genre_id == valueSelectSerie
                this.allFiltered.series = this.all.series.filter(serie => {
                    return serie.genre_ids.includes(this.valueSelectSerie);
                });
                this.popularsFiltered.series = this.populars.series.filter(serie => {
                    return serie.genre_ids.includes(this.valueSelectSerie);
                });
            }
        },
        getSearched(endPoint, query, array) {
            axios
                .get(`${this.apiStart}${endPoint}`, {
                    params: {
                        api_key: this.api_key,
                        language: this.language,
                        query: query,
                    },
                })
                .then((result) => {
                    // For each case, OBJ this.all, OBJ this.allFiltered, OBJ this.populars and OBJ this.popularsFiltered are filled
                    switch (array) {
                        case "allFilms":
                            this.all.films = result.data.results;
                            break;
                        case "allSeries":
                            this.all.series = result.data.results;
                            break;
                        case "filteredFilms":
                            this.allFiltered.films = result.data.results;
                            break;
                        case "filteredSeries":
                            this.allFiltered.series = result.data.results;
                            break;

                        // Paginate only 12 cards per array
                        case "allFilmsPopular":
                            this.populars.films = result.data.results.slice(0, 12);
                            break;
                        case "allSeriesPopular":
                            this.populars.series = result.data.results.slice(0, 12); 
                            break;
                        case "filmsPopularfiltered":
                            this.popularsFiltered.films = result.data.results.slice(0, 12);
                            break;
                        case "seriesPopularfiltered":
                            this.popularsFiltered.series = result.data.results.slice(0, 12); 
                            break;
                    }
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        search(value) {
            this.inputText = value;

            if (value != "") {
                // Display all and filtered movies and series when input:text in not empty
                this.getSearched("search/movie", this.inputText, "allFilms");
                this.getSearched("search/tv", this.inputText, "allSeries" );

                this.getSearched("search/movie", this.inputText, "filteredFilms");
                this.getSearched("search/tv", this.inputText, "filteredSeries");
            } else {
                // Display all popular films and series
                this.all.films = null;
                this.all.series = null;
            }
        },
    },
    created() {
        // Loading page
        setTimeout(() => {
            this.showMainVar = true;
        }, 500);

        // Get movies and series generes
        this.getGenres("movie", "films");
        this.getGenres("tv", "series");

        // Select genres in films and series
        this.selectGenreFilms(this.valueSelectFilm);
        this.selectGenreSeries(this.valueSelectSerie);

        // Get all and filtered trending movies and series in current day
        this.getSearched("trending/movie/day", "", "allFilmsPopular");
        this.getSearched("trending/tv/day", "", "allSeriesPopular");

        this.getSearched("trending/movie/day", "", "filmsPopularfiltered");
        this.getSearched("trending/tv/day", "", "seriesPopularfiltered");
    },
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
