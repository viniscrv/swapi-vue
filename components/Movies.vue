<script>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";

export default {
    name: "App",
    components: {
        Carousel,
        Slide,
        Pagination,
        Navigation,
    },
};
</script>

<template>
    <Carousel items-to-show="3" class="carousel" wrapAround="true" >
        <Slide v-for="slide in 6" :key="slide">
            <div class="movie-card">
                <img src="../assets/movie_posters/episode_1.jpg" alt="" />
                <strong>movie name</strong>
                <div class="movie-card__details">
                    <span>Data de lançamento</span>
                    <p>01/01/0001</p>
                    <span>Diretor</span>
                    <p>director name</p>
                </div>
            </div>
        </Slide>

        <template #addons>
            <Navigation />
            <Pagination />
        </template>
    </Carousel>
</template>

<style scoped lang="scss">

.carousel {
    margin: 2rem 0;
}
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
        transform: scale(1.02);
        transition: transform 0.3s;

        outline: 2px solid #eedb00;
    }
}
</style>
