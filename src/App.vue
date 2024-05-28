<template>
  <header>
    <h1>CRYPTO CONVERTER</h1>
  </header>
  <main>
    <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite"/>
    <div v-if="error != ''">
      <p>{{ error }}</p>
    </div>
    <div className="selectors">
      <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
      <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
    </div>
    <div v-if="result != 0">
      <h1>{{ result }}</h1>
    </div>
    <div>
      <Favourite :favs="favs" :getFromFavs="getFromFavs" v-if="favs.length > 0"/>
    </div>
  </main>
</template>

<script>
import Input from "./components/Input.vue";
import Selector from "./components/Selector.vue";
import CryptoConvert from "crypto-convert";
import Favourite from "./components/Favourite.vue";

const convert = new CryptoConvert();

export default {
  data() {
    return {
      amount: 0,
      cryptoFirst: "",
      cryptoSecond: "",
      error: "",
      result: 0,
      favs: []
    };
  },
  components: {
    Input,
    Selector,
    Favourite
  },
  methods: {
    changeAmount(val) {
      this.amount = val;
    },
    setCryptoFirst(val) {
      this.cryptoFirst = val;
    },
    setCryptoSecond(val) {
      this.cryptoSecond = val;
    },
    async convert() {
      if (this.amount <= 0) {
        this.error = "Введите число больше нуля"
        this.result = 0
        return
      } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
        this.error = "Выберите валюты"
        this.result = 0
        return
      } else if (this.cryptoFirst == this.cryptoSecond) {
        this.error = "Выберите разные типы валют"
        this.result = 0
        return
      }
      this.error = "";
      await convert.ready();
      if (this.cryptoFirst == "BTC" && this.cryptoSecond == "ETH") {
        this.result = convert.BTC.ETH(this.amount)
      } else if (this.cryptoFirst == "BTC" && this.cryptoSecond == "USD") {
        this.result = convert.BTC.USDT(this.amount)
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "BTC") {
        this.result = convert.ETH.BTC(this.amount)
      } else if (this.cryptoFirst == "ETH" && this.cryptoSecond == "USD") {
        this.result = convert.ETH.USDT(this.amount)
      } else if (this.cryptoFirst == "USD" && this.cryptoSecond == "BTC") {
        this.result = convert.USDT.BTC(this.amount)
      } else if (this.cryptoFirst == "USD" && this.cryptoSecond == "ETH") {
        this.result = convert.USDT.ETH(this.amount)
      }
    },
    favourite(){
      this.favs.push({from: this.cryptoFirst, to: this.cryptoSecond})
    },
    getFromFavs(index){
      this.cryptoFirst = this.favs[index].from
      this.cryptoSecond = this.favs[index].to
    },
  },
};
</script>

<style scoped>
.selectors {
  display: flex;
  justify-content: space-around;
  width: 500px;
  margin: 0 auto;
}
</style>
