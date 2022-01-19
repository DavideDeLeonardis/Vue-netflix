<template>
    <main>
        <Card
            v-for="(film, index) in films"
            :key="index"
            :title="film.title"
            :originalTitle="film.original_title"
            :lang="film.original_language"
            :vote="film.vote_average"
            :overview="film.overview"
        />
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
        films: {
            type: Array
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_main.scss";
</style>
