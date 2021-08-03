<template>
  <svg
    xmlns="http://www.w3.org/2000/svg"
    :class="className"
    class="absolute top-3 right-3"
    viewBox="0 0 20 20"
    fill="currentColor"
  >
    <path fill-rule="evenodd" :d="upOrDown" clip-rule="evenodd" />
  </svg>
</template>

<script>
export default {
  name: "Arrow",
  props: {
    className: {
      type: String,
      required: false,
      default: "h-5 w-5",
    },
    arrow: {
      type: String,
      required: false,
      default: "up",
    },
  },
  computed: {
    upOrDown() {
      return this.arrow === "up"
        ? "M3.293 9.707a1 1 0 010-1.414l6-6a1 1 0 011.414 0l6 6a1 1 0 01-1.414 1.414L11 5.414V17a1 1 0 11-2 0V5.414L4.707 9.707a1 1 0 01-1.414 0z"
        : "M16.707 10.293a1 1 0 010 1.414l-6 6a1 1 0 01-1.414 0l-6-6a1 1 0 111.414-1.414L9 14.586V3a1 1 0 012 0v11.586l4.293-4.293a1 1 0 011.414 0z";
    },
  },
};
</script>