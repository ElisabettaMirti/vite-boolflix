<script>
import {store} from '../store.js';
import axios from 'axios';

export default {
    data(){
        return{
            store
        }
    },
    components: {
        
    },
    props: {
        movie: {
            type: Object,
            required: true
        }
    },
    methods: {
        getImagePath: function (imgPath) {
            return new URL(imgPath, import.meta.url).href;
        },
        getMovieImg: function (imgData) {
            let imgLink = 'https://image.tmdb.org/t/p/w500' + imgData;
            return imgLink;
        },
    }
}
</script>

<template>

<p>
    Titolo : {{ movie.title || movie.name }} 
</p>
<p v-show="movie.title !== movie.original_title || movie.name !== movie.original_name">
    Titolo originale : {{ movie.original_title || movie.original_name }}
</p>
<p>
    Lingua : <img :src="getImagePath(`../assets/img/${movie.original_language}.png`)" :alt="movie.original_language">
</p>
<p>
    <span>Voto : </span>            
    <i v-for="star in (Math.ceil(store.SearchedMovie.vote_average / 2))" :key="star" class="fa-solid fa-star"></i>
</p>
<img class="movie-poster" :src="getMovieImg(movie.poster_path)" :alt="movie.title || movie.name + ' poster'">


</template>

<style lang="scss" scoped>

@use '../styles/general.scss';

img{
    width: 20px;
}

img.movie-poster{
    width: 300px;
}
</style>
