<template>
    <div v-if="quoteFrom === 'ron'">
        <!-- <h1>Ron Quote</h1> -->
        <i><h3>"{{ronQuoteDisplay[0]}}"</h3></i>
        <h2>- Ron Swanson</h2>
        <button v-on:click="onNewRonQuoteClick">New Quote</button>
    </div>
</template>

<script>
import {eventBus} from '@/main.js';


export default {
    name: "ron-quote-comp",
    props: ["ronQuoteDisplay", "quoteFrom"],
    methods: {
        onNewRonQuoteClick: function () {
            eventBus.$emit('new-ron-quote', this.ronQuoteDisplay)
        }
    }

}
</script>

<style>

</style>