<template>
  <div id="app">
    <ExtraPaymentCalculator />
  </div>
</template>

<script>
import ExtraPaymentCalculator from "./components/ExtraPaymentCalculator.vue";

export default {
  name: "app",
  components: {
    ExtraPaymentCalculator
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  font-size: 14px;
}
</style>
