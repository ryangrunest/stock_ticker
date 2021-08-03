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
      rounded-bl-2xl rounded-tr-2xl rounded-tl-md
      fixed
      bottom-5
      right-5
      w-50
      z-50
    "
    :class="borderColor"
  >
    <arrow :arrow="arrowUpOrDown" :className="iconClass"></arrow>
    <div
      class="text-xl font-medium flex flex-row justify-start width-full m-0"
      :class="`${textColor}600`"
    >
      <img class="h-12" :src="stock.logo" alt="stock ticker logo" />
      <span class="self-end pl-1">{{ stock.symbol }}</span>
    </div>
    <p class="mt-1" :class="`${textColor}500`">
      Current Price: ${{ this.stock.currentPrice }}
    </p>
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
        openPrice: 0,
        currentPrice: "...",
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
    textColor() {
      return this.increasedInValue ? "text-green-" : "text-red-";
    },
  },
  mounted() {
    if (!this.interval) {
      this.interval = setInterval(() => {
        this.updateStock();
      }, 5000);
    }
  },
  methods: {
    async updateStock() {
      let { current, open } = await this.getStockInfo();

      this.stock.currentPrice = current;
      this.stock.openPrice = open;

      if (this.stock.openPrice >= this.stock.currentPrice) {
        this.increasedInValue = false;
      } else {
        this.increasedInValue = true;
      }
    },
    getStockInfo() {
      return new Promise((resolve, reject) => {
        const config = {
          method: "GET",
          url: `https://finnhub.io/api/v1/quote?symbol=${this.stock.symbol}&token=${this.authHeader}`,
        };
        axios(config)
          .then((res) => {
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