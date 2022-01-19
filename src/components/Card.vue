<template>
    <div class="card">
        <!-- <img :src="image" :alt="title"> -->
        <ul>
            <li><span>Titolo: </span> {{ title }}</li>
            <li><span>Titolo originale: </span>{{ originalTitle }}</li>
            <li><span>Lingua: </span>{{ lang }}</li>
            <li><span>Voto: </span>{{ vote }}</li>
            <li><span>Overview: </span>{{ overview }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        // image: {
        //     type: String
        // },
        title: {
            type: String
        },
        originalTitle: {
            type: String
        },
        lang: {
            type: String
        },
        vote: {
            type: Number
        },
        overview: {
            type: String
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_card.scss";
</style>