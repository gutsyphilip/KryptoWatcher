<template>

  <div>

<h2>Current prices of coins</h2>
<div id="btc"><label>1 BTC</label><p>${{currentCurrency.BTC}}</p></div>
<div id="eth"><label>1 ETH</label><p>${{currentCurrency.ETH}}</p></div>
<div id="ltc"><label>1 LTC</label><p>${{currentCurrency.LTC}}</p></div>

  </div>

</template>

<script>
export default {
  name: 'app',

  props: {
    currentCurrency: {
      type: Object
    }
 }, 

  data () {
    return {
      pusher : '',
      prices : ''
    }
  }

}

</script>

<style scoped>

#btc {
border: 1px solid #F5CE00;
border-radius: 15px;
padding: 2em 0em;
display: inline-block;
width: 30%;
} 

#eth {
border: 1px solid #F5CE00;
border-radius: 15px;
padding: 2em 0em;
display: inline-block;
width: 30%;
}

#ltc {
border: 1px solid #F5CE00;
border-radius: 15px;
padding: 2em 0em;
display: inline-block;
width: 30%;
}

div p {
  font-size: 2rem;
}

h2 {
   font-size: 1.5em;
}

</style>
