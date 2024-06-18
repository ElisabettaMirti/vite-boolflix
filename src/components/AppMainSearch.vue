<script>
import {store} from '../store.js';
import axios from 'axios';

export default {
    data(){
        return{
            store,
            requestedMovie: ''
        }
    },
    components: {
        
    },
    props: {
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
        }
    }
}
</script>

<template>
<div class="searchbar">
    <input type="text" id="name" v-model="this.requestedMovie" @keyup="getMovie()" placeholder="Cerca un film o una serie"/>
    <i class="fa-solid fa-magnifying-glass"></i>
</div>
</template>

<style lang="scss" scoped>
@use '../styles/general.scss';

input{
    width: 250px;
    margin-right: 2rem;
    padding: .3rem;
    border: none;
    outline: none;
    border-radius: 15px;
    padding: 1em;
    background-color: #4f4f4f;
    box-shadow: inset 2px 5px 10px rgba(0,0,0,0.3);
    transition: 300ms ease-in-out;
    color: white;

    &:focus{
        background-color: white;
        color: black;
        transform: scale(1.05);
        box-shadow: 13px 13px 100px #969696,
                    -3px -3px 10px #ffffff;
    }
}


i{
    margin-right: 3rem;
}

</style>
