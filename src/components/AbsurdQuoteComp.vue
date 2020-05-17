<template>
    <div v-if="quoteFrom === 'kanye'">
        <!-- <h1>Kanye Quote</h1> -->
        <i><h3>"{{kanyeQuoteDisplay.quote}}"</h3></i>
        <h2>- Kanye West</h2>
        <button v-on:click="onNewAbsurdQuoteClick">New Quote</button>
    </div>
</template>

<script>
import {eventBus} from '@/main.js';


export default {
    name: "absurd-quote-comp",
    props: ["kanyeQuoteDisplay", "quoteFrom"],
    methods: {
        onNewAbsurdQuoteClick: function () {
            eventBus.$emit('new-kanye-quote', this.kanyeQuoteDisplay)
        }
    }
}
</script>

<style>

</style>