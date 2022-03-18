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
export default {
    name: 'Header',
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
@import "../assets/scss/_header.scss";
</style>
