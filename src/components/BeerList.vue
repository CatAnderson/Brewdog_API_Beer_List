<template>
    <form>
        <label for="selected-beer">Select Beer:</label>
            <select name="" id="selected-beer"  v-on:change='handleSelect' v-model="selectedBeer">
                <option :value="null" disabled selected>Select Beer From list</option>
                <!-- <option disabled selected value="">Select Beer From list</option> -->
                <option v-for='beer in beers' :key='beer.id' :value='beer'>{{ beer.name }}</option>
            </select>
    </form>
</template>

<script>
import { eventBus } from '@/main.js';

export default {
    name: 'beer-list',
    props: ['beers'],

    data(){
        return{
            selectedBeer: null
        }
    },

    methods:{
        handleSelect: function(){
            eventBus.$emit('selected-beer', this.selectedBeer)
        }
    }
}
</script>

<style>

</style>