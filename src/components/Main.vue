<template>
    <main>
        <div v-if="cards.films || cards.series">
            <div v-show="cards.films">
                <div class="result">I risultati della tua ricerca per "{{ inputText }}"</div>
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
        cards: {
            type: Object
        },
        inputText: {
            type: String
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_main.scss";
</style>
