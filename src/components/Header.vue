<template>
    <header>
        <span>Boolflix</span>
        <div class="container-form">
            <input 
                v-model="inputText"
                type="text" 
                placeholder="Search any film or serie"
                @keyup.enter="$emit('searchCards', inputText)"
            >
            <button @click="$emit('searchCards', inputText)">Search</button>
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {
            inputText: ''
        }
    }
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_header.scss";
</style>
