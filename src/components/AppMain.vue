<script>
import axios from 'axios';
import {store} from '../store.js';

export default {
    data(){
        return{
            store,
            requestedMovie: ''
        }
    },
    methods: {
        getMovie(){
            axios.get('https://api.themoviedb.org/3/search/movie?api_key=77858b6fb6570fc530c9dcb381e6d68f&language=it&query=' + this.requestedMovie)
            .then(function (response) {
                // handle success
                store.SearchedMovie = response.data.results;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
            axios.get('https://api.themoviedb.org/3/search/tv?api_key=77858b6fb6570fc530c9dcb381e6d68f&language=it_IT&query=' + this.requestedMovie)
            .then(function (response) {
                // handle success
                store.SearchedMovie = response.data.results;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        },
        getImagePath: function (imgPath) {
            return new URL(imgPath, import.meta.url).href;
        },
        getMovieImg: function (imgData) {
            let imgLink = 'https://image.tmdb.org/t/p/w500' + imgData;
            return imgLink;
        }
    }
}
</script>

<template>
<label for="name">Search a movie:</label>
<input type="text" id="name" v-model="this.requestedMovie" @keyup="getMovie()"/>
<input type="button" value="Cerca" @click="getMovie()"/>

<ul>
    <li v-for="(movie, index) in store.SearchedMovie" :key="index">
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
            Voto : {{ movie.vote_average.toFixed(2) }}
        </p>
        <img class="movie-poster" :src="getMovieImg(movie.poster_path)" :alt="movie.title || movie.name + ' poster'">
    </li>
</ul>
</template>

<style lang="scss">

@use '../styles/general.scss';


img{
    width: 20px;
}

img.movie-poster{
    width: 300px;
}
</style>
