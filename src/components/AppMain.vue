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
            axios.get('https://api.themoviedb.org/3/search/movie?api_key=77858b6fb6570fc530c9dcb381e6d68f&language=it&query=' + requestedMovie.replaceAll('', '+'))
            .then(function (response) {
                // handle success
                console.log(response);
                store.SearchedMovie = response;
            })
            .catch(function (error) {
                // handle error
                console.log(error);
            })
            .finally(function () {
                // always executed
            });
        }
    }
}
</script>

<template>
<label for="name">Search a movie:</label>
<input type="text" id="name" v-model="this.requestedMovie"/>
<input type="button" value="Cerca" @click="getMovie()"/>

<ul>
    <li v-for="(movie, index) in store.SearchedMovie" :key="index">
        {{ store.SearchedMovie.title }}
    </li>
</ul>
</template>

<style lang="scss">

@use '../styles/general.scss';
</style>
