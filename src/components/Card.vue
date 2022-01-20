<template>
    <div>
        <div 
            class="card"
            @mouseover="showInfo = true" 
            @mouseleave="showInfo = false"
        >
            <img 
                :src="`https://image.tmdb.org/t/p/w342/${image}`" 
                :alt="title ? title : name"
            >
            <ul v-show="showInfo">
                <li><span>Titolo: </span>{{ title ? title : name }}</li>
                <li><span>Titolo originale: </span>{{ originalTitle ? originalTitle : originalName }}</li>
                <li><span>Lingua: </span>{{ lang }}</li>
                <li><span>Voto: </span>{{ vote }}</li>
                <li><span>Overview: </span>{{ overview }}</li>
            </ul>
        </div>
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
        image: {
            type: String
        },
        title: {
            type: String
        },
        originalTitle: {
            type: String
        },
        name: {
            type: String
        },
        originalName: {
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
