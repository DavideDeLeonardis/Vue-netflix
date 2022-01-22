<template>
    <main>
        <div v-if="cards.films || cards.series">
            <div class="result">I risultati della tua ricerca per "{{ inputText }}"</div>

            <div v-show="cards.films">
                <h1 v-if="cards.films.length > 0">Film</h1>
                <div v-else class="else">Nessun film corrisponde alla tua ricerca</div>
                <div class="cards">
                    <Card
                        v-for="(film, index) in cards.films"
                        :key="`A${index}`"
                        :list="film"
                    />
                </div>
            </div>

            <div v-show="cards.series">
                <h1 v-if="cards.series.length > 0">Serie</h1>
                <div v-else class="else">Nessuna serie corrisponde alla tua ricerca</div>
                <div class="cards">
                    <Card
                        v-for="(serie, index) in cards.series"
                        :key="`B${index}`"
                        :list="serie"
                    />
                </div>
            </div>
        </div>

        <div v-else>
            <h1>FILM PIÚ POPOLARI</h1>
            <div class="cards">
                <Card
                    v-for="(film, index) in populars.films"
                    :key="`C${index}`"
                    :list="film"
                />
            </div>

            <h1>SERIE PIÚ POPOLARI</h1>
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
import Card from './Card.vue'

export default {
    name: 'Main',
    components: {
        Card
    },
    props: {
        inputText: {
            type: String
        },
        cards: {
            type: Object
        },
        populars: {
            type: Object
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_main.scss";
</style>
