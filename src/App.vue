<template lang="html">
  <main class="main-container">

    <h1 class="main-title">Witch's Brew(Dog)</h1>

    <section class='beer-selection'>
      <beer-list v-if='beers.length' :beers='beers'></beer-list>

      <button v-if='!favouriteBeers.includes(selectedBeer)' v-on:click='addToFavourites'>Add Beer</button>

      <beer-detail v-if="selectedBeer" :beer='selectedBeer'></beer-detail>
    </section>

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
    fetch('https://api.punkapi.com/v2/beers?page=2&per_page=80')
    .then(response => response.json())
    .then(data => this.beers = data);

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer
    })

    eventBus.$on('selected-favourite-beer', (beer) => {
      this.favouriteBeers.splice(this.favouriteBeers.indexOf(beer), 1)
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
    },
  }
}
</script>

<style lang="css" scoped>

  .main-container {
    font-family: 'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    width: 100vw;
    height: 50vh;
    display: grid;
    grid-template-columns: 50% 50%;
    margin: 0px;
    text-align: center;
}

  .main-title{
    font-size: 60pt;
    grid-column:  1 / -1;
    background-color: #000000;
    padding: 30px;
    margin: 0px;
    color: #ffffff;
  }

  .beer-selection{
    display: block;
    color: antiquewhite;
    background-image: linear-gradient(to right, #03001e, #7303c0, #ec38bc);
    height: 100vh;
    padding: 30px;
  }

</style>