<template>
    <header>
        <span>Boolflix</span>
        <input 
            v-model="inputText"
            type="text" 
            placeholder="Search any film or serie"
            @keyup="$emit('searchCards', inputText)"
        >
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
