<template>
  <div class="container">
    <stock-ticker></stock-ticker>
  </div>
</template>

<script>
import StockTicker from "@/components/StockTicker.vue";

export default {
  components: { StockTicker },
  name: "App",
};
</script>