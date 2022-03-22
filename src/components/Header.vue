<template>
    <header>
        <span>Boolflix</span>
        <div class="header-right">
            <div class="container-select">
                <h4 style="color: white">Filtra FILM per genere</h4>
                <select
                    v-model="valueSelectFilm"
                    @change="$emit('emitSelectFilm', valueSelectFilm)"
                >
                    <option value="tutti">Tutti</option>
                    <option
                        v-for="(genre, index) in genres.films"
                        :key="`E${index}`"
                        :value="genre.id"
                    >
                        {{ genre.name }}
                    </option>
                </select>
            </div>

            <div class="container-select">
                <h4 style="color: white">Filtra SERIE per genere</h4>
                <select
                    v-model="valueSelectSerie"
                    @change="$emit('emitSelectSerie', valueSelectSerie)"
                >
                    <option value="tutte">Tutte</option>
                    <option
                        v-for="(genre, index) in genres.series"
                        :key="`F${index}`"
                        :value="genre.id"
                    >
                        {{ genre.name }}
                    </option>
                </select>
            </div>

            <input
                v-show="showInputVar"
                v-model="inputText"
                type="text"
                placeholder="Cerca"
                @keyup="$emit('search', inputText)"
            />

            <font-awesome-icon
                v-show="!showInputVar"
                @click="showInputVar = true"
                icon="search"
            />
        </div>
    </header>
</template>

<script>
export default {
    name: "Header",
    data() {
        return {
            inputText: "",
            valueSelectFilm: "tutti",
            valueSelectSerie: "tutte",
            showInputVar: false,
        };
    },
    props: {
        genres: {
            type: Object,
            default() {
                return {};
            },
        },
    },
};
</script>

<style scoped lang="scss">
@import "../assets/scss/_header.scss";
</style>
