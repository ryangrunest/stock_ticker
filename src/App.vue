<template>
  <div class="container">
    <stock-ticker :authHeader="authHeader"></stock-ticker>
  </div>
</template>

<script>
import StockTicker from "@/components/StockTicker.vue";

export default {
  components: { StockTicker },
  name: "App",
  computed: {
    authHeader() {
      return process.env.VUE_APP_AUTH_HEADER;
    },
  },
};
</script>