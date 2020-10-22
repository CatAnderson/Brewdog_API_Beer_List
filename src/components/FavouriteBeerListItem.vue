<template lang="html">
<section class='fav-beers'>
    <h2> Favourite Beers...</h2>
    <ul>
        <li v-for='favouriteBeer in favouriteBeers' :key='favouriteBeer.id' v-model="selectedFavouriteBeer">{{ favouriteBeer.name }} <img :src="favouriteBeer.image_url" alt="beer pic" class='small-beer'>
        <br>
        <button v-on:click="updateBeer(favouriteBeer)">Remove From Favourites</button>
        </li>
    </ul>
</section>
</template>

<script>
import { eventBus } from '@/main.js'

export default {
    name: 'favourite-beers',
    props: ['favouriteBeers'],

    data(){
        return{
            selectedFavouriteBeer: null
        }  
    },

    methods: {
        // removeBeer: function() {
        //     this.favouriteBeers.remove(favouriteBeer)
        // }

        updateBeer: function(beer) {
            this.selectedFavouriteBeer = beer;

            eventBus.$emit('selected-favourite-beer', this.selectedFavouriteBeer)
        }

    }

}
</script>

<style lang="css" scoped>

    .fav-beers {
        background-image: linear-gradient(to right,#00f260,#0575e6);
        padding: 30px;
        color: #ffffff;
        justify-content: center;
}

.small-beer {
    height :15vh
}
 ul {
    text-decoration: none;
    list-style: none;
 }

li {
    display: flex;
    flex-flow: row wrap;
}
</style>