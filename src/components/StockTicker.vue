<template>
  <div
    class="
      p-4
      mx-auto
      bg-white
      dark:bg-black
      flex flex-col
      shadow-md
      hover:shadow-xl
      border-2
      rounded-t rounded-l
      fixed
      bottom-5
      right-5
      z-50
    "
    :class="borderColor"
  >
    <arrow :arrow="arrowUpOrDown" :className="iconClass"></arrow>
    <div
      class="
        text-xl
        font-medium
        text-black
        flex flex-row
        justify-start
        width-full
        m-0
      "
    >
      <img class="h-12" :src="stock.logo" alt="stock ticker logo" />
      <span class="self-end pl-1">{{ stock.symbol }}</span>
    </div>
    <p class="text-gray-500 m-0">Current Price: $14</p>
  </div>
</template>

<script>
import axios from "axios";
import Arrow from "./icons/ArrowIcon.vue";

export default {
  components: { Arrow },
  name: "StockTicker",
  props: {
    authHeader: {
      type: String,
      required: false, // change to true
      default: "c445tlaad3iftpcmujr0", // remove this before building for prod
    },
  },
  data() {
    return {
      increasedInValue: true,
      stock: {
        symbol: "AAPL",
        openPrice: 261.07,
        currentPrice: 261.74,
        logo: "https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Ftse1.mm.bing.net%2Fth%3Fid%3DOIP.gSY2HU_gD2tnys1rdRmY1AHaIJ%26pid%3DApi&f=1",
      },
    };
  },
  computed: {
    iconClass() {
      return this.increasedInValue
        ? "h-5 w-5 text-green-500"
        : "h-5 w-5 text-red-500";
    },
    arrowUpOrDown() {
      return this.increasedInValue ? "up" : "down";
    },
    borderColor() {
      return this.increasedInValue ? "border-green-500" : "border-red-500";
    },
  },
  mounted() {
    this.updateStock();
  },
  methods: {
    async updateStock() {
      console.log("updating stock");
      let { open, current } = await this.getStockInfo();
      console.log(open, current);
      //
    },
    getStockInfo() {
      return new Promise((resolve, reject) => {
        const config = {
          method: "GET",
          url: `https://finnhub.io/api/v1/quote?symbol=${this.stock.symbol}&token=${this.authHeader}`,
        };
        axios(config)
          .then((res) => {
            console.log(res.data);
            resolve({ open: res.data.o, current: res.data.c });
          })
          .catch((err) => reject(err));
      });
    },
  },
};
</script>

<style>
</style>