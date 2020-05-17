<!-- MVP
1 The application should display data from an API request.
2 The application should have a clear separation of concerns (multiple components)
3 Take input from the user to update the page. You could update the page by filtering 
or manipulating the data on user interaction, or you might make further API requests 
to load more data that is then displayed
-->


<template>

  <div class="body">
    <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Jost">

    <div class="centered">
      <h1>Quotes for a Tired Mind</h1>
      <p><i>It is a pleasure to be able to quote lines to fit any occasion..."</i> - Abraham Lincoln</p>
        <div class="select-name">
          <button v-on:click="handleSelectName('programming')">Programming</button>
          <button v-on:click="handleSelectName('ron')">Stoic Inspiration</button>
          <button v-on:click="handleSelectName('kanye')">Absurd</button>
          <button v-on:click="handleSelectName('trump')">Dumb</button>
        </div>
    </div>
    <div class="display">
      <prog-quote-comp :progQuoteDisplay="progQuote" :quoteFrom="quoteFrom"></prog-quote-comp>
      <ron-quote-comp :ronQuoteDisplay="ronQuote" :quoteFrom="quoteFrom"></ron-quote-comp>
      <absurd-quote-comp :kanyeQuoteDisplay="absurdQuote" :quoteFrom="quoteFrom"></absurd-quote-comp>
      <dumb-quote-comp :trumpQuoteDisplay="dumbQuote" :quoteFrom="quoteFrom"></dumb-quote-comp>
    </div>
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

body {
  font-family: Jost;
  color: white;
  text-shadow: 2px 2px 15px rgb(34, 34, 34);
  justify-content: center;
  background: rgb(147, 135, 255) url('./assets/IMG_3372.png');
  background-size: 100%;
}

button {
    padding:5px 15px; 
    margin: 10px;
    background:rgb(46, 144, 209); 
    border:0 none;
    cursor:pointer;
    -webkit-border-radius: 5px;
    border-radius: 5px; 
    font-family: Jost;
    color: white;
    text-shadow: 1px 1px 5px grey;
    font-size:18px;
    box-shadow: 1px 1px 4px rgb(145, 221, 245);
}

.centered {
    position: relative;
    /* top: 100%; */
    left: 0%;
    /* transform: translate(-50%, -50%); */
    text-align: center;
}

.display {

  text-align: center;
  margin-left: 300px;
  margin-right: 300px;

}


</style>
