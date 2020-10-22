<template lang="html">
<aside>
    <h2> Favourite Beers...</h2>
    <ul>
        <li v-for='favouriteBeer in favouriteBeers'>{{ favouriteBeer.name }} <img :src="favouriteBeer.image_url" alt="beer pic" class='small-beer'></li>
    </ul>
</aside>
</template>

<script>
export default {
    name: 'favourite-beers',
    props: ['favouriteBeers']

}
</script>

<style lang="css" scoped>

</style>