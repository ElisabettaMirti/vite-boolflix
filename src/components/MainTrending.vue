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

<h1>In tendenza</h1>

<div class="movie-container">
    <article v-for="(element, i) in store.TrendingShow" :key="i">
        <div>
            <img class="movie-poster" v-if="element.poster_path == null"  src="..//assets/img/img_not_found.jpg" alt="Image not found">
            <img class="movie-poster" v-else :src="getMovieImg(element.poster_path)" :alt="element.title || element.name + ' poster'">
        </div>

        <div class="card-back">
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
                <i v-for="(star, index) in (5 - Math.floor(element.vote_average / 2))" :key="index" class="fa-regular fa-star"></i>
            </p>
        </div>  
        
    </article>
</div>


</template>

<style lang="scss" scoped>

@use '../styles/general.scss';

div.movie-container{
    display: flex;
    align-items: start;
    justify-content: space-between;
    padding: 0 2rem;
    overflow-y: scroll;
}


article{
    margin-bottom: 3rem;
    margin-right: 1rem;
    width: calc((100vw / 6) - 1rem);
    position: relative;

    &:hover div.card-back{            
        display: flex;
        flex-direction: column;
        justify-content: end;
        padding: 2rem .5rem;
        background-color: rgb(0, 0, 0, 0.8);
        animation: card_info .5s linear;        
    }
}

.card-back{
    display: none;
    position: absolute;
    height: 100%;
    width: -moz-available;
    bottom: 0;
    left: 0;
}


img{
    width: 20px;
}

img.movie-poster{
    width: calc((100vw / 6) - 1rem);
}


@keyframes card_info {
    0%{
        height: 0%;
        background-color:rgb(0, 0, 0, 0.1);
    }
    100%{
        height: 100%;
        background-color:rgb(0, 0, 0, 0.8);
    }
    
}

</style>
