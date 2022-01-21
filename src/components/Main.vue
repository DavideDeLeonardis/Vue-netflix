<template>
    <main>
        <div v-if="cards.films.length != 0">
            <h1>Film</h1>
            <div class="cards">
                <Card
                    v-for="(film, index) in cards.films"
                    :key="`A${index}`"
                    :list="film"
                />
            </div>
        </div>
        <div v-else class="else">Nessun film corrisponde alla tua ricerca</div>

        <div v-if="cards.series.length != 0">
            <h1>Serie</h1>
            <div class="cards">
                <Card
                    v-for="(serie, index) in cards.series"
                    :key="`B${index}`"
                    :list="serie"
                />
            </div>
        </div>
        <div v-else class="else">Nessuna serie corrisponde alla tua ricerca</div>
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
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_main.scss";
</style>
