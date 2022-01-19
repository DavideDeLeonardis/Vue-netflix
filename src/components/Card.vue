<template>
    <div 
        class="card"
        @mouseover="showInfo = true" 
        @mouseleave="showInfo = false"
    >
        <ul v-show="showInfo">
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
    data() {
        return {
            showInfo: false
        }
    },
    props: {
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
