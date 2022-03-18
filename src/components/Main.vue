<template>
    <main>
        <div v-if="all.films || all.series">
            <div class="result">I risultati della tua ricerca per "{{ inputText }}"</div>

            <div v-show="all.films">
                <h1 v-if="all.films && all.films.length > 0">Film</h1>
                <div v-else class="else">Nessun film corrisponde alla tua ricerca</div>
                <div class="cards">
                    <Card
                        v-for="(film, index) in all.films"
                        :key="`A${index}`"
                        :list="film"
                    />
                </div>
            </div>

            <div v-show="all.series">
                <h1 v-if="all.series && all.series.length > 0">Serie</h1>
                <div v-else class="else">Nessuna serie corrisponde alla tua ricerca</div>
                <div class="cards">
                    <Card
                        v-for="(serie, index) in all.series"
                        :key="`B${index}`"
                        :list="serie"
                    />
                </div>
            </div>
        </div>

        <div v-else>
            <h1>FILM PIÚ VISTI OGGI</h1>
            <div class="cards">
                <Card
                    v-for="(film, index) in populars.films"
                    :key="`C${index}`"
                    :list="film"
                />
            </div>

            <h1>SERIE PIÚ VISTE OGGI</h1>
            <div class="cards">
                <Card
                    v-for="(serie, index) in populars.series"
                    :key="`D${index}`"
                    :list="serie"
                />
            </div>
        </div>
    </main>
</template>

<script>
import Card from './Card.vue';

export default {
    name: 'Main',
    components: {
        Card
    },
    props: {
        inputText: {
            type: String
        },
        all: {
            type: Object
        },
        populars: {
            type: Object
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/_main.scss";
</style>
