<template>
  <div
    class="
      p-6
      mx-auto
      bg-white
      dark:bg-black
      flex
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
      <div class="text-xl font-medium text-black">AAPL</div>
      <p class="text-gray-500">Current Price: $14</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "StockTicker",
};
</script>

<style>
</style>