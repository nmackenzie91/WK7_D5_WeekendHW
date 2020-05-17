<!-- MVP
1 The application should display data from an API request.
2 The application should have a clear separation of concerns (multiple components)
3 Take input from the user to update the page. You could update the page by filtering 
or manipulating the data on user interaction, or you might make further API requests 
to load more data that is then displayed
-->


<template>
  <div>
    <div>
      <h1>Random Quote</h1>
        <div class="select-name">
          <h3 v-on:click="handleSelectName('programming')">Programming</h3>
          <h3 v-on:click="handleSelectName('ron')">Ron</h3>
        </div>
    </div>


    <prog-quote-comp :progQuoteDisplay="progQuote" :quoteFrom="quoteFrom"></prog-quote-comp>


    <ron-quote-comp :ronQuoteDisplay="ronQuote1" :quoteFrom="quoteFrom"></ron-quote-comp>
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
      ronQuote1: {},
      absurdQuote: {},
      quoteFrom: ""
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
      .then(banana => this.ronQuote1 = banana)
    },

    getAbsurdQuote: function() {
      fetch("https://api.tronalddump.io/random/quote")
  
      .then(res => res.json())
      .then(absurdQuote => this.absurdQuote = absurdQuote)
    },
    handleSelectName(banana) {
      this.quoteFrom = banana
    }


    // getAbsurdQuote1: function() {
    //   fetch("https://api.tronalddump.io/random/quote")
  
    //   .then(res => res.json())
    //   .then(absurdQuote1 => this.absurdQuote1 = absurdQuote1)
    // },

    // getAbsurdQuote2: function() {
    //   fetch("https://api.kanye.rest/")

    //   .then(res => res.json())
    //   .then(absurdQuote2 => this.absurdQuote2 = absurdQuote2)
    // }

  },
  mounted(){
    this.getProgQuote();
    this.getRonQuote();
    this.getAbsurdQuote();
    // this.getAbsurdQuote1();
    // this.getAbsurdQuote2();

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
