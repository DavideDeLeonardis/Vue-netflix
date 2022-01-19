<template>
    <main>
        <div class="card">
            <img src="" alt="">
        </div>
        <div class="card">
            <img src="" alt="">
        </div>
        <div class="card">
            <img src="" alt="">
        </div>
    </main>
</template>

<script>
export default {
    name: 'Main'
}
</script>

<style scoped lang="scss">
@import "../assets/scss/partials/_mixins.scss";

main {
    @include flex(row, $justify: center, $align: initial, $wrap: true, $gap: 50px);
    width: 95%;
    margin: 1.5em auto;
    .card {
        width: 200px;
        height: 300px;
        border: 1px solid red;
        padding: 20px;
    }
}
</style>
