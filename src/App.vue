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
    <quote-comp :quoteDisplay="quote"></quote-comp>
  </div>
</template>

<script>
import QuoteComp from './components/QuoteComp.vue';


export default {
  name: 'app',
  data() {
    return{
      quote: {}
    };
  },
  methods: {

  },
  mounted(){
    fetch("https://programming-quotes-api.herokuapp.com/quotes/random")
    .then(res => res.json())
    .then(quote => this.quote = quote)
  },
  components: {
    "quote-comp": QuoteComp
  }

}
</script>

<style>

</style>
