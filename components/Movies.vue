<script setup>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";

const { data: movies } = await useFetch("https://swapi.dev/api/films/");
</script>

<template>
    <main>
        <Carousel items-to-show="3" class="carousel" wrapAround="true">
            <Slide v-for="movie in movies.results" :key="movie.episode_id">
                <div class="movie-card">
                    <img
                        src="../assets/movie_posters/episode_2.jpg"
                        :alt="`${movie.title}`"
                    />
                    <strong>{{ movie.title }}</strong>
                    <div class="movie-card__details">
                        <span>Data de lançamento</span>
                        <p>{{ movie.release_date }}</p>
                        <span>Diretor</span>
                        <p>{{ movie.director }}</p>
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
.movie-card {
    width: 300px;
    display: flex;
    flex-direction: column;
    align-items: start;
    border: 3px solid #505059;
    border-radius: 6px;
    cursor: pointer;

    img {
        width: 100%;
        object-fit: cover;
    }
    .movie-card__details {
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
