<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in products" v-bind:key="product">
      <h3>{{ product }}</h3>
    </div>
  </div>
</template>
<style></style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("/api/products").then((response) => {
        this.products = response.data;
        console.log("all products:", this.products);
      });
    },
  },
};
</script>
