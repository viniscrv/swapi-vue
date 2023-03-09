<script setup>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";

const { data: characters } = await useFetch("https://swapi.dev/api/people");
</script>

<template>
    <main>
        <Carousel items-to-show="3" class="carousel" wrapAround="true">
            <Slide
                v-for="character in characters.results"
                :key="character.name"
            >
                <div class="character-card">
                    <strong>{{ character.name }}</strong>
                    <div class="character-card__details">
                        <span>Data de nascimento</span>
                        <p>{{ character.birth_year }}</p>
                        <span>Altura</span>
                        <p>{{ character.height }}</p>
                    </div>
                </div>
            </Slide>

            <template #addons>
                <Navigation />
                <Pagination />
            </template>
        </Carousel>
    </main>
</template>

<style scoped lang="scss">
.character-card {
    width: 300px;
    display: flex;
    flex-direction: column;
    align-items: start;
    border: 3px solid #505059;
    border-radius: 6px;
    cursor: pointer;
    .character-card__details {
        padding: 1rem;
        text-align: left;
        display: flex;
        flex-direction: column;
        gap: 0.3rem;

        span {
            font-weight: bold;
        }
    }

    strong {
        background-color: #29292e;
        width: 100%;
        padding: 1rem;
    }

    &:hover {
        /* transform: scale(1.02);
        transition: transform 0.3s; */

        border: 3px solid #eedb00;
    }
}
</style>
