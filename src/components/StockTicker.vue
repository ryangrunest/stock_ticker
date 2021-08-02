<template>
  <div
    class="
      p-6
      mx-auto
      bg-white
      dark:bg-black
      flexa
      shadow-md
      hover:shadow-xl
      items-center
      border-2 border-red-200
      rounded-t rounded-l
      space-x-3
      fixed
      bottom-5
      right-5
      z-50
    "
  >
    <div class="flex-shrink-0">
      <img class="h-12 w-12" src="@/assets/aapl.jpeg" alt="ChitChat Logo" />
    </div>
    <div>
      <div class="text-xl font-medium text-black">
        <span>AAPL</span>
        <arrow :className="iconClass"></arrow>
      </div>
      <p class="text-gray-500">Current Price: $14</p>
    </div>
  </div>
</template>

<script>
import Arrow from "./icons/ArrowIcon.vue";

export default {
  components: { Arrow },
  name: "StockTicker",
  data() {
    return {
      increasedInValue: true,
    };
  },
  computed: {
    iconClass() {
      return this.increasedInValue
        ? "h-5 w-5 text-green-500"
        : "h-5 w-5 text-red-500";
    },
  },
};
</script>

<style>
</style>