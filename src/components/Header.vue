<template>
    <header>
        <span>Boolflix</span>

        <div>
            <select></select>
            <button>Search</button>
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header'
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_mixins.scss";

header {
    @include flex(row, $justify: space-between, $align: center, $wrap: false, $gap: 0);
    height: 70px;
    background-color: rgb(0, 0, 0);
    padding: 0 20px;
    span {
        font-size: 1.2em;
        text-transform: uppercase;
        color: rgb(255, 0, 0);
    }
}
</style>
