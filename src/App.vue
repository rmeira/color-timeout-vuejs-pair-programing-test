<template>
  <div class="wrapper">
    Timeout total: {{ totalTimeout }}
    <div
      class="item"
      v-for="({ color }, index) in colors"
      :key="index"
      :style="`background-color: ${color};`"
    ></div>
  </div>
</template>

<script>
import data from "../data.json";
export default {
  name: "App",
  data() {
    return {
      colors: [],
      totalTimeout: 0,
      data,
    };
  },
  mounted() {
    this.handleColors();
  },
  methods: {
    handleColors() {
      if (this.data.length) {
        const item = this.data[0];

        setTimeout(() => {
          this.colors = [...this.colors, item];
          this.totalTimeout = this.totalTimeout + item.timeout;
          this.data.shift();
          this.handleColors();
        }, item.timeout);
      }
    },
  },
};
</script>

<style>
.wrapper {
  display: flex;
  flex-direction: column;
  width: 100%;
}
.item {
  width: 96%;
  height: 200px;
  border: 1px solid #ccc;
}
</style>
