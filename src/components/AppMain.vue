<script>
import axios from 'axios';
import {store} from '../store.js';

export default {
    data(){
    return{
        store
    }
    }
}
</script>

<template>
<label for="name">Search a movie:</label>
<input type="text" id="name" />
</template>

<style lang="scss">

@use '../styles/general.scss';
</style>
