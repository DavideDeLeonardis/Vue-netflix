<template>
    <div 
        class="card"
        @mouseover="showInfo = true" 
        @mouseleave="showInfo = false"
    >
        <img v-if="image"
            :src="`https://image.tmdb.org/t/p/w342/${image}`" 
            :alt="title ? title : name"
        >
        <div v-else class="else">
            IMMAGINE NON DISPONIBILE
            <div><span>Titolo: </span><br>{{ title ? title : name }}</div>
        </div>
        <ul v-show="showInfo">
            <li><span>Titolo: </span>{{ title ? title : name }}</li>
            <li v-show="title != originalTitle || name != originalName">
                <span>Titolo originale: </span>{{ originalTitle ? originalTitle : originalName }}
            </li>
            <li>
                <span>Lingua originale: </span>
                <img
                    v-if="isAvailable"
                    :src="require(`../assets/img/${lang}.png`)"
                    :alt="title ? title : name"
                >
                <div v-else class="language">{{ lang }}</div>
            </li>
            <li><span>Voto: </span>{{ vote }}</li>
            <li>
                <span>Overview: </span>
                <div v-if="overview">{{ overview }}</div>
                <div v-else>NON DISPONIBILE</div>  
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    name: 'Card',
    data() {
        return {
            showInfo: false,
            availableLang: [
                'it',
                'en',
                'fr',
                'ja'
            ]
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
    },
    computed: {
        isAvailable() {
            if (this.availableLang.includes(this.lang)) {
                return true;
            }
            return false;
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_card.scss";
</style>
