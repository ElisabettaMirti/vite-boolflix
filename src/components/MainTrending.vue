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

<article class="card">
    <div class="card-content card-front">
        <img class="movie-poster" :src="getMovieImg(element.poster_path)" :alt="element.title || element.name + ' poster'">
    </div>

    <div class="info card-content card-back">
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
    </div>
    
    
</article>

</template>

<style lang="scss" scoped>

@use '../styles/general.scss';



article{
    margin-bottom: 3rem;
    padding: 1rem;
    width: calc((100vw / 5) - 1rem);
    height: 450px;
}

.card {
    perspective: 1000px;
    width: 300px;
    position:relative;
}

.card-content {
    box-shadow: 0 2rem 2rem rgba(0, 0, 0, .5);
    transition: all 2s;
    position:absolute;
    top:0;
    left:0;
    width:100%;
    height: 100%;
    backface-visibility: hidden;
}

.card-back{
    transform:rotateY(180deg);
}

.card:hover .card-front {
    transform: rotateY(-180deg);
}

.card:hover .card-back {
    transform: rotateY(0);
}


img{
    width: 20px;
}

img.movie-poster{
    width: 100%;
}

</style>
