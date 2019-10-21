<template>
  <div>
    <Navbar></Navbar>
    <div class="container mt-4">
    <div class="row">
      <div class="col-md-7">
        <div class="row">
          <div class="col-md-6" :key="product.id" v-for="product in products">
            <product
              :isInCart="isInCart(product)"
              v-on:add-to-cart="addToCart(product)"
              :product="product"
            ></product>
          </div>
        </div>
      </div>
      <div class="col-md-5 my-5">
        <cart v-on:pay="pay()" v-on:remove-from-cart="removeFromCart($event)" :items="cart"></cart>
      </div>
    </div>
  </div>
  </div>
  
</template>

<script>
//import products from "@/products.json";
import Product from "@/components/Product.vue";
import Navbar from "@/components/Navbar.vue";
import Cart from "@/components/Cart.vue";

const axios = require('axios');

export default {
  name: "app",
  components: {
    Product,
    Cart,
    Navbar
  },
  data() {
    return {
      products:[],
      cart: []
    };
  },
  methods: {
    addToCart(product) {
      this.cart.push(product);
    },
    isInCart(product) {
      const item = this.cart.find(item => item.id === product.id);
      if (item) {
        return true;
      }
      return false;
    },
    removeFromCart(product) {
      this.cart = this.cart.filter(item => item.id !== product.id);
    },
    pay() {
      this.cart = [];
      alert("Thanks! Shopping successfully completed. ");
    }
  },
  mounted() {
    axios
      .get("http://dummy.restapiexample.com/api/v1/employees")
      .then(data => (this.products= data.data));
  }
};
</script>

<style>
body {
  background-color: #dcdcdc;
}
</style>


