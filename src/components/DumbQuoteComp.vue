<template>
    <div v-if="quoteFrom === 'trump'">
        <i><h3>"{{trumpQuoteDisplay.value}}"</h3></i>
        <!-- <p>- {{trumpQuoteDisplay._embedded.author[0].name}}</p> -->
        <p>- Donald Trump</p>
        <button v-on:click="onNewDumbQuoteClick">New Quote</button>

    </div>

</template>

<script>
import {eventBus} from '@/main.js';

export default {
    name: "dumb-quote-comp",
    props: ["trumpQuoteDisplay", "quoteFrom"],
    methods: {
        onNewDumbQuoteClick: function () {
            eventBus.$emit('new-trump-quote', this.trumpQuoteDisplay)
        }
    }
}
</script>

<style>

</style>