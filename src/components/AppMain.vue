<script>
import axios from 'axios';
import {store} from '../store.js';
import SingleArticle from './SingleArticle.vue';
import MainTrending from './MainTrending.vue';
import AppHeader from './AppHeader.vue'

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
        },

        getSuggested: function(){
            axios.get('https://api.themoviedb.org/3/trending/all/day?api_key=77858b6fb6570fc530c9dcb381e6d68f&language=it&page=2')
            .then(function (response) {
                // handle success
                store.suggested = response.data.results;
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
        this.getSuggested();
    }
}
</script>

<template>
<AppHeader/>

<SingleArticle v-if="store.SearchedMovie.length > 0"/>
<MainTrending v-else />    

</template>

<style lang="scss">
@use '../styles/general.scss';


</style>
