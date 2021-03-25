<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      Title:
      <input type="text" v-model="newProductTitle" />
      Price:
      <input type="text" v-model="newProductPrice" />
      Description:
      <input type="text" v-model="newProductDescription" />
      Inventory:
      <input type="text" v-model="newProductInventory" />
      Supplier Id:
      <input type="text" v-model="newProductSupplierId" />
      Image Url:
      <input type="text" v-model="newProductImageUrl" />

      <button v-on:click="addProduct">Add Product</button>
    </div>

    <div v-for="product in products" v-bind:key="product">
      <h3>{{ product.name }}</h3>
      <img v-bind:src="product.image_url" v-bind:alt="product.name" />
      <p>{{ product.description }}</p>
      <p>{{ product.price }}</p>
    </div>
  </div>
</template>
<style>
body {
  background-color: yellow;
}
img {
  max-width: 250px;
  border: dotted;
}
</style>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      NewProductTitle: "",
      NewProductPrice: "",
      NewProductDescription: "",
      NewProductInventory: "",
      NewProductSupplierId: "",
      NewProductImageUrl: "",
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
    addProduct: function () {
      console.log("creating product..");
      var params = {
        title: this.NewProductTitle,
        price: this.NewProductPrice,
        inventory: this.NewProductInventory,
        supplier_id: this.newProductId,
        image_url: this.newProductImageUrl,
      };
      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>
