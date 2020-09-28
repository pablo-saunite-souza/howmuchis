<template>
  <div id="app">
    <div class="container pt-3">
      <h1>How Much Is</h1>
      <h3>Your better online currency conversor</h3>
    </div>
    <div id="dashboard" class="container">
      <div class="d-flex row justify-content-center align-items-center">
        <Conversor v-bind:coins="coins" v-bind:price="price" v-on:convert="convert" />
      </div>
    </div>
    <div class="card mt-2 shadow bg-white rounded fixed-bottom">
      <div class="card-body">
        <h5 class="card-title">How Much is</h5>
        <p class="card-text">
          Donate: my Acounts...
        </p>
        <p class="card-text">
          <small class="text-muted">Copyright 2020 - ©howmuchis<br>Powered by Pablo Saunite de Souza.</small>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import Conversor from "./components/Conversor.vue";

const urlCoins = `https://olinda.bcb.gov.br/olinda/servico/PTAX/versao/v1/odata/Moedas?$top=100&$format=json&$select=simbolo`

const getToday = () => {
  let today = `${new Date().getMonth()+1}-${new Date().getDate()}-${new Date().getFullYear()}`;
  if (new Date().getHours() <10 && new Date().getMinutes() < 30){
      today = `${new Date().getMonth()+1}-${new Date().getDate()-1}-${new Date().getFullYear()}`;
  }
  return today;
};

const getUrl = (currency, today) => {
  const url = `https://olinda.bcb.gov.br/olinda/servico/PTAX/versao/v1/odata/CotacaoMoedaDia(moeda=@moeda,dataCotacao=@dataCotacao)?@moeda='`+currency+`'&@dataCotacao='`+today+`'&$top=100&$format=json`
  return url;
};
export default {
  name: 'App',
  components: {
    Conversor
  },
  data(){
    return {
      coins: [],
      price: ""
    };
  },
  methods: {
    async getCoins(){
      const response = await fetch(urlCoins, {
        method: "GET",
        mode: 'cors',
        cache: 'no-cache',
        headers: {
          'Content-Type': 'application/json',
        },
      });
      const data = await response.json();
      data.value.map( coin => {
        this.coins.push(coin.simbolo);
      });
      this.coins.push("BRL")
    },
    async getPrice(currency, amaut){
      if (!currency){
        alert("No currency provided.");
      }
      const response = await fetch(getUrl(currency, getToday()), {
        method: "GET",
        mode: 'cors',
        cache: 'no-cache',
        headers: {
          'Content-Type': 'application/json',
        }
      });
      const data = await response.json();
      const quotes = data.value.map( quote => {
        return {hour: quote.dataHoraCotacao.split(" ")[1].split(":")[0], value: quote.cotacaoVenda};
      });
      for(let i = 0; i < quotes.length; i++ ){
        if (i+1 == quotes.length){
          this.price = Number(amaut / (quotes[i].value)).toFixed(2);
        }
      }
    },

    async getParity(currency, amaut){
      if (!currency){
        alert("No currency provided.");
      }
      const response = await fetch(getUrl(currency, getToday()), {
        method: "GET",
        mode: 'cors',
        cache: 'no-cache',
        headers: {
          'Content-Type': 'application/json',
        }
      });
      const data = await response.json();
      const quotes = data.value.map( quote => {
        return {hour: quote.dataHoraCotacao.split(" ")[1].split(":")[0], value: quote.paridadeVenda};
      });
      for(let i = 0; i < quotes.length; i++ ){
        if (i+1 == quotes.length){
          this.price = Number(amaut / (quotes[i].value)).toFixed(2);
        }
      }
    },

    async convert({coinA, coinB, amaut}){
      if (coinA === coinB){
        return this.price = amaut;
      }
      if (coinA !== "BRL"){
        return await this.getParity(coinB, amaut);
      }
      if (coinB === "BRL"){
        return await this.getPrice(coinA, amaut);
      }
      return await this.getPrice(coinB, amaut);
    }
  },
  created(){
    this.getCoins();
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #ddd;
  width: 100vw;
  height: 100vh;
}

.container {
  margin-left: auto;
  margin-right: auto;
  margin-top: auto;
  margin-bottom: auto;
}

</style>