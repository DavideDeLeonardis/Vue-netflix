<template>
    <div 
        class="card"
        @mouseover="showInfoVar = true" 
        @mouseleave="showInfoVar = false"
    >
        <img v-if="list.poster_path"
            :src="`https://image.tmdb.org/t/p/w342/${list.poster_path}`" 
            :alt="list.title ? list.title : list.name"
        >
        <div v-else class="else">
            IMMAGINE NON DISPONIBILE
            <div><span>Titolo: </span><br>{{ list.title ? list.title : list.name }}</div>
        </div>
        <ul v-show="showInfoVar">
            <li><span>Titolo: </span>{{ list.title ? list.title : list.name }}</li>
            <li v-show="list.title != list.original_title || list.name != list.original_name">
                <span>Titolo originale: </span>{{ list.original_title ? list.original_title : list.original_name }}
            </li>
            <li>
                <span>Lingua originale: </span>
                <img
                    v-if="isAvailable"
                    :src="require(`../assets/img/${list.original_language}.png`)"
                    :alt="list.title ? list.title : list.name"
                >
                <p v-else>{{ list.original_language }}</p>
            </li>
            <li><span>Voto: </span>{{ getStars() }} / 5</li>
            <li>
                <span>Overview: </span>
                <div v-if="list.overview">{{ list.overview }}</div>
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
            showInfoVar: false,
            availableLang: [
                'it',
                'en',
                'fr',
                'ja'
            ]
        }
    },
    props: {
        list: {
            type: Object
        }
    },
    computed: {
        isAvailable() {
            if (this.availableLang.includes(this.list.original_language)) {
                return true;
            }
            return false;
        }
    },
    methods: {
        getStars() {
            return Math.ceil(this.list.vote_average / 2);
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_card.scss";
</style>
