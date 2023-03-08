<script setup>
import Movies from "../components/Movies.vue";
</script>

<template>
    <main>
        <h2>Movies</h2>
        <div>
            <Movies />
        </div>
        <h2>Characters</h2>
        <div></div>
    </main>
</template>

<style scoped lang="scss">
main {
    width: 1200px;
    text-align: center;
    margin: 0 auto;

    h2 {
        font-size: 2rem;
        margin: 2rem 0;
    }
}
</style>
