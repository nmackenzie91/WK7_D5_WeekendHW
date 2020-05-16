<template>
    <div>
        <i><h3>"{{progQuoteDisplay.en}}"</h3></i>
        <p>- {{progQuoteDisplay.author}}</p>
        <button v-on:click="onNewProgQuoteClick">New Quote</button>
    </div>
</template>

<script>
import {eventBus} from '@/main.js';


export default {
    name: "prog-quote-comp",
    props: ["progQuoteDisplay"],
    methods: {
        onNewProgQuoteClick: function () {
            eventBus.$emit("new-prog-quote", this.progQuoteDisplay)
        }
    }
}
</script>

<style>

</style>