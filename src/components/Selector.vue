<template>
  <ul>
    <li @click="setCrypto('BTC')":className="cryptoNow == 'BTC' ? 'active' : ''">Bitcoin</li>
    <li @click="setCrypto('ETH')":className="cryptoNow == 'ETH' ? 'active' : ''">ETH</li>
    <li @click="setCrypto('USD')" :className="cryptoNow == 'USD' ? 'active' : ''">USDT</li>
  </ul>
</template>

<script>
export default {
  props: {
    setCrypto: {
      type: Function,
      required: true,
    },
    cryptoNow: {
      type: String,
      required: true
    }
  }
};
</script>

<style scoped></style>
