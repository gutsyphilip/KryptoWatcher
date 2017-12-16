<template>

  <div>

<h2>Previous prices of coins</h2>
<div id="first" v-for="day in previousCurrency">
<h2>Date: &nbsp; {{day.DATE}}</h2>
<p><label>1 BTC:&nbsp;</label>{{day.BTC}}</p>
<p><label>1 ETH:&nbsp;</label>{{day.ETH}}</p>
<p><label>1 LTC:&nbsp;</label>{{day.LTC}}</p>
</div>
 </div>

</template>

<script>

export default {
  name: 'app',

    props: {
    previousCurrency: {
      type: Array
    }
 }, 

  data () {
    return {

    }
  }
}

</script>

<style scoped>
*{
  color:rgb(0, 193, 131);
}

#first, #second, #third, #fourth, #fifth {
border: 1px solid rgb(0, 193, 131);
box-shadow: 2px 2px 2px 2px #929292;
padding: 2em 0em;
max-width: 90%;
margin: 10px  auto;
} 

#first p, #second p, #third p, #fourth p, #fifth p {
  display: inline-block;
  padding: 0em 1.5em;
  font-size: 1.5rem;
}

h2 {
  text-transform: uppercase;
   font-size: 1.5em;

}

</style>
