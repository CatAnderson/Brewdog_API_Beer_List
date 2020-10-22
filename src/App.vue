<template lang="html">
  <main>
    <h1>Brewdog App</h1>

    <beer-list v-if='beers.length' :beers='beers'></beer-list>

    <button v-if='!favouriteBeers.includes(selectedBeer)' v-on:click='addToFavourites'>Add Beer</button>

    <beer-detail v-if="selectedBeer" :beer='selectedBeer'></beer-detail>
    <hr>
    <favourite-beers :favouriteBeers='favouriteBeers'></favourite-beers>
  </main>
</template>

<script>

import BeerList from "./components/BeerList.vue"
import BeerDetail from "./components/BeerDetail.vue"
import FavouriteBeerListItem from "./components/FavouriteBeerListItem.vue"
import { eventBus } from '@/main.js';

export default {
  name: 'App',

  data(){
    return{
      beers: [],
      selectedBeer: null,
      favouriteBeers:[]
    }
  },  
  
  mounted(){
    fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
    .then(response => response.json())
    .then(data => this.beers = data);

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer
  })
  },

  components:{
    'beer-list': BeerList,
    'beer-detail': BeerDetail,
    'favourite-beers': FavouriteBeerListItem
  },

  methods: {
    addToFavourites: function(){
      this.favouriteBeers.push(this.selectedBeer);
    }
  }
}
</script>

<style lang="css" scoped>

</style>