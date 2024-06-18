<script>
import axios from 'axios';
import {store} from '../store.js';
import SingleArticle from './SingleArticle.vue';
import MainTrending from './MainTrending.vue';
import AppHeader from "./AppHeader.vue"

export default {
    data(){
        return{
            store
        }
    },
    components: {
        SingleArticle,
        MainTrending,
        AppHeader
    },
    methods: {
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
<AppHeader/>

<div class="movie-container">    
    <SingleArticle v-if="store.SearchedMovie.length > 0" v-for="(element, index) in store.SearchedMovie" :key="index" :movie="element"/>
    <MainTrending v-else v-for="(element, i) in store.TrendingShow" :key="i" :element="element"/>    
</div>
</template>

<style lang="scss">

@use '../styles/general.scss';

</style>
