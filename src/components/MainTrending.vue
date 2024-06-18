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
        element: {
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
<div class="trending-container">
    <article >
    <p>
        Titolo : {{element.title || element.name }} 
    </p>
    <p v-show="element.title !== element.original_title || element.name !== element.original_name">
        Titolo originale : {{ element.original_title || element.original_name }}
    </p>
    <p>
        Lingua : <img :src="getImagePath(`../assets/img/${element.original_language}.png`)" :alt="element.original_language">
    </p>
    <p>
        <span>Voto : </span>            
        <i v-for="(star, index) in (Math.ceil(element.vote_average / 2))" :key="index" class="fa-solid fa-star"></i>
    </p>
    <img class="movie-poster" :src="getMovieImg(element.poster_path)" :alt="element.title || element.name + ' poster'">

</article>
</div>
</template>

<style lang="scss" scoped>

@use '../styles/general.scss';

article{
    border: 1px solid grey;
    border-radius: .5rem;
    margin-bottom: 1rem;
    padding: 1rem;
}

img{
    width: 20px;
}

img.movie-poster{
    width: 300px;
}

</style>
