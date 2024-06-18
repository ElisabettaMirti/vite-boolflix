<script>
import axios from 'axios';
import {store} from '../store.js';
import SingleArticle from './SingleArticle.vue';
import MainTrending from './MainTrending.vue'

export default {
    data(){
        return{
            store,
            requestedMovie: ''
        }
    },
    components: {
        SingleArticle,
        MainTrending
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
        getTrending: function(){
            axios.get('https://api.themoviedb.org/3/trending/all/day?api_key=77858b6fb6570fc530c9dcb381e6d68f&language=it')
            .then(function (response) {
                // handle success
                store.TrendingShow = response.data.results;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        }
    },
    created(){
        this.getTrending();
    }
}
</script>

<template>
<label for="name">Search a movie:</label>
<input type="text" id="name" v-model="this.requestedMovie" @keyup="getMovie()"/>
<input type="button" value="Cerca" @click="getMovie()"/>

<div class="movie-container">
    
    <SingleArticle v-if="store.SearchedMovie.length > 0" v-for="(element, index) in store.SearchedMovie" :key="index" :movie="element"/>
    <MainTrending v-else v-for="(element, i) in store.TrendingShow" :key="i" :element="element"/>    
</div>
</template>

<style lang="scss">

@use '../styles/general.scss';

</style>
