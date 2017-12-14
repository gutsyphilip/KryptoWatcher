<template>

  <div>

  <div id="header">
   <img src="/src/assets/favicon.png" height="55px" width="55px">
   <h2>KRYPTO-WATCHER</h2>
  </div>


  <div id="body"> 
  <h2> KRYPTO-WATCHER is a realtime PWA that displays updates on cryptocurrencies</h2>
  <div id="current"> <current v-bind:currentCurrency="currentCurrency"> </current>  </div>
  <div id="previous"> <previous v-bind:previousCurrency="previousCurrency"> </previous>  </div>
  </div>

  </div>

</template>

<script>

import Current from './components/Current.vue';
import Previous from './components/Previous.vue';
import Pusher from 'pusher-js'

export default {

  name: 'app',

  components: {
    current: Current,
    previous: Previous
  },

  data () {

    return {

      currentCurrency: {
      BTC : '',
      ETH : '',
      LTC : '',
      },

      previousCurrency: {
        yesterday: {},
        twoDays: {},
        threeDays: {},
        fourDays: {},
        fiveDays: {}
      }
    }
  },

  methods: {

  yesterdayPrices: function() {

    var self = this;    
    var date = this.$moment().subtract(1, 'days').unix();

    this.axios.all([
      
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=BTC&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=ETH&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=LTC&tsyms=USD&ts=' + date)

    ]).then(this.axios.spread((BTC, ETH, LTC) => {

                let temp  = {

                    DATE: this.$moment.unix(date).format("MMMM Do YYYY"),
                    BTC: BTC.data.BTC.USD,
                    ETH: ETH.data.ETH.USD,
                    LTC: LTC.data.LTC.USD
                }

                self.previousCurrency.yesterday = temp;
                localStorage.setItem('yesterdayPrices', JSON.stringify(temp));

            }))

  },

  twoDaysPrices: function() {

    var self = this;
    var date = this.$moment().subtract(2, 'days').unix();    

    this.axios.all([
      
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=BTC&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=ETH&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=LTC&tsyms=USD&ts=' + date)

    ]).then(this.axios.spread((BTC, ETH, LTC) => {

                let temp  = {

                    DATE: this.$moment.unix(date).format("MMMM Do YYYY"),
                    BTC: BTC.data.BTC.USD,
                    ETH: ETH.data.ETH.USD,
                    LTC: LTC.data.LTC.USD
                }

                self.previousCurrency.twoDays = temp;
                localStorage.setItem('twoDaysPrices', JSON.stringify(temp));

            }))

  },

  threeDaysPrices: function() {

    var self = this;
    var date = this.$moment().subtract(3, 'days').unix();    

    this.axios.all([
      
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=BTC&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=ETH&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=LTC&tsyms=USD&ts=' + date)

    ]).then(this.axios.spread((BTC, ETH, LTC) => {

                let temp  = {

                    DATE: this.$moment.unix(date).format("MMMM Do YYYY"),
                    BTC: BTC.data.BTC.USD,
                    ETH: ETH.data.ETH.USD,
                    LTC: LTC.data.LTC.USD
                }

                self.previousCurrency.threeDays = temp;
                localStorage.setItem('threeDaysPrices', JSON.stringify(temp));

            }))

  },

  fourDaysPrices: function(date) {

    var self = this;
    var date = this.$moment().subtract(4, 'days').unix();        

    this.axios.all([
      
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=BTC&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=ETH&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=LTC&tsyms=USD&ts=' + date)

    ]).then(this.axios.spread((BTC, ETH, LTC) => {

                let temp  = {

                    DATE: this.$moment.unix(date).format("MMMM Do YYYY"),
                    BTC: BTC.data.BTC.USD,
                    ETH: ETH.data.ETH.USD,
                    LTC: LTC.data.LTC.USD
                }

                self.previousCurrency.fourDays = temp;
                localStorage.setItem('fourDaysPrices', JSON.stringify(temp));

            }))

  },

fiveDaysPrices: function() {

    var self = this;
    var date = this.$moment().subtract(5, 'days').unix(); 

    this.axios.all([
      
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=BTC&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=ETH&tsyms=USD&ts=' + date),
       this.axios.get('https://min-api.cryptocompare.com/data/pricehistorical?fsym=LTC&tsyms=USD&ts=' + date)

    ]).then(this.axios.spread((BTC, ETH, LTC) => {

                let temp  = {

                    DATE: this.$moment.unix(date).format("MMMM Do YYYY"),
                    BTC: BTC.data.BTC.USD,
                    ETH: ETH.data.ETH.USD,
                    LTC: LTC.data.LTC.USD
                }

                self.previousCurrency.fiveDays = temp;
                localStorage.setItem('fiveDaysPrices', JSON.stringify(temp));

            }))

  },


    sendPricePusher (data) {
        this.axios.post('/api/prices/update', {
            update: data
        })
            .then(response => {
                console.log(response)
            })
            .catch(error => {
                console.log(error)
            })
    }

  },

 created(){

       if (!navigator.onLine) {

        this.currentCurrency.BTC = localStorage.getItem('BTC');
        this.currentCurrency.ETH = localStorage.getItem('ETH');
        this.currentCurrency.LTC = localStorage.getItem('LTC');

        this.previousCurrency.yesterday = JSON.parse(localStorage.getItem('yesterdayPrices'))
        this.previousCurrency.twoDays = JSON.parse(localStorage.getItem('twoDaysPrices'))
        this.previousCurrency.threeDays = JSON.parse(localStorage.getItem('threeDaysPrices'))
        this.previousCurrency.fourDays = JSON.parse(localStorage.getItem('fourDaysPrices'))
        this.previousCurrency.fiveDays = JSON.parse(localStorage.getItem('fiveDaysPrices'))
    }

    this.pusher = new Pusher('92328e0f11b44cfe765f', {
      cluster: 'eu',
      encrypted: true
    });

   this.prices = this.pusher.subscribe('price-updates');

    this.yesterdayPrices()
    this.twoDaysPrices()
    this.threeDaysPrices()
    this.fourDaysPrices()
    this.fiveDaysPrices()

    this.axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,LTC&tsyms=USD').then((response) => {

    this.currentCurrency.BTC = response.data.BTC.USD,
    localStorage.setItem('BTC', response.data.BTC.USD),

    this.currentCurrency.ETH = response.data.ETH.USD,
    localStorage.setItem('ETH', response.data.ETH.USD),

    this.currentCurrency.LTC = response.data.LTC.USD,
    localStorage.setItem('LTC', response.data.LTC.USD)
})

  },

  mounted(){
    
       setInterval(() => {
            this.axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms=BTC,ETH,LTC&tsyms=USD')
                .then(response => {
                    this.sendPricePusher (response.data)
                })
                .catch(error => {
                    console.log(error)
                })
        }, 5000);


  this.prices.bind('coin-updates', update => {
            this.currentCurrency.BTC =  update.update.BTC.USD
            this.currentCurrency.ETH =  update.update.ETH.USD
            this.currentCurrency.LTC =  update.update.LTC.USD
        });

  }

}


</script>

<style scoped>

* {
  margin : 0px;
  padding : 0px;
  box-sizing: border-box;
}

body, html {
  height: 100%;
  width: 100%;
}

#header {
  background: #4F4F4F;
  padding: 1em;
  margin-bottom: 1em;
  text-align: center;
}

#header h2 {
  color: white;
  font-weight: bold;
  font-size: 2rem;
}

#body {
  max-width: 90%;
  margin: 0 auto;
  padding: 1.5em;
  background: #4F4F4F;
  text-align: center;
}

#body h2{ 
  color: white;
}

#current {
  padding: 2em 0em;
}

#previous {
  padding: 2em 0em;
}
</style>
