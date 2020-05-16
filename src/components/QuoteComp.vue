<template>
    <div>
        <i><h3>"{{quoteDisplay.en}}"</h3></i>
        <p>- {{quoteDisplay.author}}</p>
        <button v-on:click="onNewQuoteClick">New Quote</button>
    </div>
</template>

<script>
import {eventBus} from '@/main.js';


export default {
    name: "quote-comp",
    props: ["quoteDisplay"],
    methods: {
        onNewQuoteClick: function () {
            eventBus.$emit("new-quote", this.quoteDisplay)
        }
    }
}
</script>

<style>

</style>