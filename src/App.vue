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
      <h1>Distract my Mind with Quotes</h1>
        <div class="select-name">
          <button v-on:click="handleSelectName('programming')">Programming</button>
          <button v-on:click="handleSelectName('ron')">Stoic Inspiration</button>
          <button v-on:click="handleSelectName('kanye')">Absurd</button>
          <button v-on:click="handleSelectName('trump')">Dumb</button>
        </div>
    </div>

    <prog-quote-comp :progQuoteDisplay="progQuote" :quoteFrom="quoteFrom"></prog-quote-comp>
    <ron-quote-comp :ronQuoteDisplay="ronQuote" :quoteFrom="quoteFrom"></ron-quote-comp>
    <absurd-quote-comp :kanyeQuoteDisplay="absurdQuote" :quoteFrom="quoteFrom"></absurd-quote-comp>
    <dumb-quote-comp :trumpQuoteDisplay="dumbQuote" :quoteFrom="quoteFrom"></dumb-quote-comp>
  </div>
</template>

<script>
import DumbQuote from './components/DumbQuoteComp.vue';
import AbsurdQuote from './components/AbsurdQuoteComp.vue';
import RonQuoteComp from './components/RonQuoteComp.vue';
import ProgQuoteComp from './components/ProgQuoteComp.vue';
import {eventBus} from '@/main.js';


export default {
  name: 'app',
  data() {
    return{
      progQuote: {},
      ronQuote: {},
      absurdQuote: {},
      dumbQuote: {},
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
      .then(banana => this.ronQuote = banana)
    },

    getAbsurdQuote: function() {
      fetch("https://api.kanye.rest")
      .then(res => res.json())
      .then(absurdQuote => this.absurdQuote = absurdQuote)
    },

    getDumbQuote: function() {
      fetch("https://api.tronalddump.io/random/quote")  
      .then(res => res.json())
      .then(dumbQuote => this.dumbQuote = dumbQuote)
    },

    handleSelectName(name) {
      this.quoteFrom = name
    },




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
    this.getDumbQuote();
    // this.getAbsurdQuote1();
    // this.getAbsurdQuote2();

    eventBus.$on("new-prog-quote", () => this.getProgQuote());
    eventBus.$on("new-ron-quote", () => this.getRonQuote());
    eventBus.$on("new-kanye-quote", () => this.getAbsurdQuote());
    eventBus.$on("new-trump-quote", () => this.getDumbQuote());
  },
  components: {
    "prog-quote-comp": ProgQuoteComp,
    "ron-quote-comp": RonQuoteComp,
    "absurd-quote-comp": AbsurdQuote,
    "dumb-quote-comp": DumbQuote
  }

}
</script>

<style>

</style>
