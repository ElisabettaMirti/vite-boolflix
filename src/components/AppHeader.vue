<script>
import {store} from '../store.js';
import AppMainSearch from './AppMainSearch.vue'

export default {
    data(){
        return{
            store
        }
    },
    components: {
        AppMainSearch
    },
    props: {
    },
    methods: {
    }
}
</script>

<template>

<header>
    <div class="navbar">
        <img src="../assets/img/512px-Netflix_2015_logo.svg.png" alt="">
        <nav>
            <ul>
                <li>Home</li>
                <li>Serie TV</li>
                <li>Film</li>
                <li>Originali</li>
                <li>Aggiunti di recente</li>
                <li>La mia lista</li>
            </ul>
        </nav>
    </div>


    <AppMainSearch/>
</header>

</template>

<style lang="scss" scoped>
@use '../styles/general.scss';

header{
    height: 120px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

div.navbar{
    display: flex;
    justify-content: center;
    align-items: center;

    img{
        height: 60px;
        margin: 0 3rem;
    }

    ul{
        display: flex;
        align-items: center;
        
        li{
            margin-right: 1rem;
            color: rgb(195, 193, 193);

            &:hover{
                color: white;
                cursor: pointer;
            }
        }
    }
}

</style>
