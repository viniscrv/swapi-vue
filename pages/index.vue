<script setup>
import Movies from "../components/Movies.vue";
import Characters from "~~/components/Characters.vue";
</script>

<template>
    <Head>
        <Title>Star Wars Universe</Title>
    </Head>
    <main>
        <h2>Movies</h2>
        <Movies />
        <h2>Characters</h2>
        <Characters />
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
