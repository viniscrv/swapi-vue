<script setup>
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Pagination, Navigation } from "vue3-carousel";
import episode1 from "../../assets/movie_posters/episode_1.jpg";
import episode2 from "../../assets/movie_posters/episode_2.jpg";
import episode3 from "../../assets/movie_posters/episode_3.jpg";
import episode4 from "../../assets/movie_posters/episode_4.jpg";
import episode5 from "../../assets/movie_posters/episode_5.jpg";
import episode6 from "../../assets/movie_posters/episode_6.jpg";

const moviePosters = [
    episode1,
    episode2,
    episode3,
    episode4,
    episode5,
    episode6,
];

const { id } = useRoute().params;

const { data: movie } = await useFetch(`https://swapi.dev/api/films/${id}/`);

/* ALL CHARACTERS */
const { data: characters } = await useFetch("https://swapi.dev/api/people");
</script>

<script>
export default {
    data() {
        return {
            reviews: [
                {
                    name: "John Doe",
                    message: "Very good!",
                },
            ],
            name: "",
            message: "",
        };
    },
    methods: {
        publishReview: function (e, name, message) {
            e.preventDefault();
            this.reviews.push({ name, message });
            this.name = "";
            this.message = "";
        },
    },
};
</script>

<template>
    <main>
        <h2>{{ movie.title }}</h2>
        <div>
            <div class="content">
                <h3>Description</h3>

                <p>{{ movie.opening_crawl }}</p>

                <div class="content-details">
                    <strong>Data de lançamento</strong>
                    <span>{{ movie.release_date }}</span>

                    <strong>Diretor</strong>
                    <span>{{ movie.director }}</span>

                    <strong>Productor</strong>
                    <span>{{ movie.producer }}</span>
                </div>
            </div>
            <img :src="moviePosters[movie.episode_id - 1]" />
        </div>

        <h2>Characters of the movie</h2>

        <!-- ALL CHARATERS -->
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

        <h2>Write a review</h2>

        <form>
            <div>
                <label for="name">Your name</label>
                <input type="text" id="name" v-model="name" />
            </div>
            <div>
                <label for="review">Review</label>
                <textarea id="review" v-model="message" />
            </div>

            <button @click="publishReview($event, name, message)">
                Publish
            </button>
        </form>

        <h2>Reviews</h2>

        <div class="reviews-box">
            <div v-for="review in reviews" :key="review">
                <span
                    ><strong>{{ review.name }}</strong> posted:</span
                >
                <p>{{ review.message }}</p>
            </div>
        </div>
    </main>
</template>

<style scoped lang="scss">
main {
    width: 1200px;
    margin: 0 auto;

    h2 {
        font-size: 2rem;
        text-align: center;
        margin: 4rem 0;
    }
    div {
        display: flex;
        justify-content: space-between;
        .content {
            width: 60%;
            display: flex;
            justify-content: flex-start;
            flex-direction: column;
            gap: 1.5rem;
            h3 {
                font-size: 1.5rem;
            }
            p {
                font-size: 1.1rem;
            }
            .content-details {
                display: flex;
                flex-direction: column;
                strong {
                    font-size: 1.1rem;
                }
                span {
                    font-size: 1.02rem;
                }
            }
        }
        img {
            width: 300px;
            border-radius: 8px;
        }
    }
}
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
        border: 3px solid #eedb00;
    }
}

form {
    display: grid;
    grid-template-columns: 1fr;
    gap: 0.5rem;
    div {
        display: flex;
        flex-direction: column;
        gap: 0.8rem;
        width: 100%;
    }
    label {
        font-size: 1.2rem;
    }
    input,
    textarea {
        background-color: #29292e;
        border: 2px solid #505059;
        border-radius: 6px;
        padding: 1rem;
        color: #cdcdcd;
    }
    textarea {
        resize: vertical;
    }
    button {
        background-color: #eedb00;
        padding: 15px 30px;
        border: 0;
        border-radius: 6px;
        cursor: pointer;
        font-weight: bold;
    }
}

.reviews-box {
    margin: 2rem 0;
    display: flex;
    flex-direction: column;

    div {
        border-bottom: 2px solid #505059;
        display: flex;
        flex-direction: column;
        gap: 0.5rem;
        padding: 10px;
        width: 100%;

        span {
            font-size: 1.1rem;
        }

        &:first-child {
            border-top: 2px solid #505059;
        }
    }
}
</style>
