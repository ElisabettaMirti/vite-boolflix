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
                Titolo : <strong class="title">{{ element.title || element.name }} </strong> 
            </p>
            <p v-show="element.title !== element.original_title || element.name !== element.original_name">
                Titolo originale : {{ element.original_title || element.original_name }}
            </p>
            <p class="lang">
                <span>Lingua originale: </span>
                <span>
                    <img :src="getImagePath(`../assets/img/${element.original_language}.png`)" :alt="element.original_language">
                </span>
            </p>
            <p>
                <span>Voto : </span>            
                <i v-for="(star, index) in (Math.ceil(element.vote_average / 2))" :key="index" class="fa-solid fa-star"></i>
                <i v-for="(star, index) in (5 - Math.ceil(element.vote_average / 2))" :key="index" class="fa-regular fa-star"></i>
            </p>
            <p>
                Overview : {{ element.overview }}
            </p>
        </div>  
        
    </article>
</div>

<h1>Suggeriti per te</h1>

<div class="movie-container">
    <article v-for="(element, index) in store.suggested" :key="index">
        <div>
            <img class="movie-poster" v-if="element.poster_path == null"  src="..//assets/img/img_not_found.jpg" alt="Image not found">
            <img class="movie-poster" v-else :src="getMovieImg(element.poster_path)" :alt="element.title || element.name + ' poster'">
        </div>

        <div class="card-back">
            <p>
                Titolo : <strong class="title"> {{element.title || element.name }} </strong> 
            </p>
            <p v-show="element.title !== element.original_title || element.name !== element.original_name">
                Titolo originale : {{ element.original_title || element.original_name }}
            </p>
            <p class="lang">
                <span>Lingua originale: </span>
                <span>
                    <img :src="getImagePath(`../assets/img/${element.original_language}.png`)" :alt="element.original_language">
                </span>
            </p>
            <p>
                <span>Voto : </span>            
                <i v-for="(star, index) in (Math.ceil(element.vote_average / 2))" :key="index" class="fa-solid fa-star"></i>
                <i v-for="(star, index) in (5 - Math.ceil(element.vote_average / 2))" :key="index" class="fa-regular fa-star"></i>
            </p>
            <p>
                Overview : {{ element.overview }}
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

h1{
    margin: 2rem;
}

p{
    font-size: .8rem;
    margin-bottom: .5rem;
}

p.lang{
    display: flex;
    align-items: center;

    span{
        margin-right: .3rem;
    }
}

.title{
    font-size: 1rem;
}

article{
    margin-bottom: 3rem;
    margin-right: 1rem;
    width: calc((100vw / 6) - 1rem);
    position: relative;
    cursor: pointer;

    &:hover div.card-back{            
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
        padding: 2rem .5rem;
        background-color: rgba(0, 0, 0, 0.85);
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
