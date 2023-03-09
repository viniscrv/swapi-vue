<script setup>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";
import episode1 from "../assets/movie_posters/episode_1.jpg";
import episode2 from "../assets/movie_posters/episode_2.jpg";
import episode3 from "../assets/movie_posters/episode_3.jpg";
import episode4 from "../assets/movie_posters/episode_4.jpg";
import episode5 from "../assets/movie_posters/episode_5.jpg";
import episode6 from "../assets/movie_posters/episode_6.jpg";

const moviePosters = [
    episode1,
    episode2,
    episode3,
    episode4,
    episode5,
    episode6,
];

const { data: movies } = await useFetch("https://swapi.dev/api/films/");
</script>

<template>
    <main>
        <Carousel
            items-to-show="3"
            class="carousel"
            wrapAround="true"
            snapAlign="start"
        >
            <Slide
                v-for="(movie, index) in movies.results"
                :key="movie.episode_id"
            >
                <NuxtLink :to="`/Movie/${index + 1}`" class="movie-card">
                    <img
                        :src="moviePosters[movie.episode_id - 1]"
                        :alt="`${movie.title}`"
                    />
                    <strong>{{ movie.title }}</strong>
                    <div class="movie-card__details">
                        <span>Data de lançamento</span>
                        <p>{{ movie.release_date }}</p>
                        <span>Diretor</span>
                        <p>{{ movie.director }}</p>
                    </div>
                </NuxtLink>
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
    text-decoration: none;
    color: #cdcdcd;

    img {
        width: 100%;
        height: 394px;
        object-fit: cover;
        border-top-left-radius: 6px;
        border-top-right-radius: 6px;
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
        border: 3px solid #eedb00;
    }
}
</style>
