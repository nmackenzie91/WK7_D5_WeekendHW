<!-- MVP
1 The application should display data from an API request.
2 The application should have a clear separation of concerns (multiple components)
3 Take input from the user to update the page. You could update the page by filtering 
or manipulating the data on user interaction, or you might make further API requests 
to load more data that is then displayed
-->


<template>
  <div>
    <h1>Programming Quotes</h1>
    <prog-quote-comp :progQuoteDisplay="progQuote"></prog-quote-comp>
    
    <h1>Another Quote</h1>
    <ron-quote-comp :ronQuoteDisplay="ronQuote"></ron-quote-comp>
  </div>
</template>

<script>
import RonQuoteComp from './components/RonQuoteComp.vue';
import ProgQuoteComp from './components/ProgQuoteComp.vue';
import {eventBus} from '@/main.js';


export default {
  name: 'app',
  data() {
    return{
      progQuote: {},
      ronQuote: {}
    };
  },
  methods: {
    getProgQuote: function() {
      fetch("https://programming-quotes-api.herokuapp.com/quotes/random")
      .then(res => res.json())
      .then(progQuote => this.progQuote = progQuote)
    },

    getRonQuote: function() {
      fetch("https://ron-swanson-quotes.herokuapp.com/v2/quotes")
      .then(res => res.json())
      .then(ronQuote => this.ronQuote = ronQuote)
    },

  },
  mounted(){
    this.getProgQuote();
    this.getRonQuote();

    eventBus.$on("new-prog-quote", () => this.getProgQuote());
    eventBus.$on("new-ron-quote", () => this.getRonQuote());
  },
  components: {
    "prog-quote-comp": ProgQuoteComp,
    "ron-quote-comp": RonQuoteComp
  }

}
</script>

<style>

</style>
