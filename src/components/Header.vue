<template>
    <header>
        <span>Boolflix</span>
        <div class="header-right">
            <span href="#">Film</span>
            <span href="#">Serie</span>
            <!-- <select 
                v-model="valueSelect"
            >
                <option disabled value="">Seleziona un genere</option>
                <option value="all">Tutti</option>
                <option
                    v-for="(genre, index) in genres.films"
                    :key="`E${index}`"
                    :value="genre"
                >
                    {{ genre.name }}
                </option>
            </select> -->

            <input
                v-show="showInputVar"
                v-model="inputText"
                type="text" 
                placeholder="Cerca"
                @keyup="$emit('search', inputText)"
            >

            <font-awesome-icon 
                v-show="!showInputVar"
                @click="showInputVar = true"
                icon="search"
            />
        </div>
    </header>
</template>

<script>
import { library } from '@fortawesome/fontawesome-svg-core';
import { faSearch } from '@fortawesome/free-solid-svg-icons';
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
library.add(faSearch);

export default {
    name: 'Header',
    components: {
        FontAwesomeIcon
    },
    data() {
        return {
            inputText: '',
            // valueSelect: '',
            showInputVar: false
        }
    },
    props: {
        // genres: {
        //     type: Object
        // }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_header.scss";
</style>
