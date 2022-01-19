<template>
    <div id="app">
        <Header

        />
        <Main

        />
    </div>
</template>

<script>
import Header from "./components/Header.vue";
import Main from "./components/Main.vue";

export default {
    name: "App",
    components: {
        Header,
        Main,
    },
    data() {
        return {
            
        }
    },
    methods: {

    }
};
</script>

<style lang="scss">
@import "./assets/scss/partials/_commons.scss";
</style>
