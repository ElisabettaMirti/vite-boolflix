<script>
import axios from 'axios';
import {store} from '../store.js';
import SingleArticle from './SingleArticle.vue'

export default {
    data(){
        return{
            store,
            requestedMovie: ''
        }
    },
    components: {
        SingleArticle
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
        },
        getStarRate: function (MovieRate) {
            let stars = store.SearchedMovie.vote_average;
            stars = Number.parseInte(MovieRate) / 2;
            return stars;
        }
    }
}
</script>

<template>
<label for="name">Search a movie:</label>
<input type="text" id="name" v-model="this.requestedMovie" @keyup="getMovie()"/>
<input type="button" value="Cerca" @click="getMovie()"/>

<div class="movie-conainer">
    <SingleArticle v-for="(movie, index) in store.SearchedMovie" :key="index" :movie="movie"/>
</div>
</template>

<style lang="scss">

@use '../styles/general.scss';


img{
    width: 20px;
}

img.movie-poster{
    width: 300px;
}

article{
    border: 1px solid grey;
    border-radius: .5rem;
    margin-bottom: 1rem;
    padding: 1rem;
}
</style>
