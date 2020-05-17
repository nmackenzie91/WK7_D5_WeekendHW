<template>
    <div v-if="quoteFrom === 'programming'">
        <!-- <h1>Programming Quotes</h1> -->
        <i><h3>"{{progQuoteDisplay.en}}"</h3></i>
        <h2>- {{progQuoteDisplay.author}}</h2>
        <button v-on:click="onNewProgQuoteClick">New Quote</button>
    </div>
</template>

<script>
import {eventBus} from '@/main.js';


export default {
    name: "prog-quote-comp",
    props: ["progQuoteDisplay", "quoteFrom"],
    methods: {
        onNewProgQuoteClick: function () {
            eventBus.$emit("new-prog-quote", this.progQuoteDisplay)
        }
    }
}
</script>

<style>

</style>