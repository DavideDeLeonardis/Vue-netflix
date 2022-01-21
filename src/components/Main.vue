<template>
    <main>
        <div v-if="cards.films.length != 0">
            <h1>Film</h1>
            <div class="cards">
                <Card
                    v-for="(film, index) in cards.films"
                    :key="`A${index}`"
                    :image="film.poster_path"
                    :title="film.title"
                    :originalTitle="film.original_title"
                    :lang="film.original_language"
                    :vote="film.vote_average"
                    :overview="film.overview"
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
                    :image="serie.poster_path"
                    :name="serie.name"
                    :originalName="serie.original_name"
                    :lang="serie.original_language"
                    :vote="serie.vote_average"
                    :overview="serie.overview"
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
