<template>
  <div class="app">
    <div class="container">
      <h1>Shopping Page</h1>
      <div class="card" v-if="searchedProduct">
        <input type="text" id="input-search" placeholder="Find Something?" v-model="searchTerm">
        <button type="submit" @click="search" class="find">Find</button><br><br>
        <img :src="searchedProduct.img" :alt="searchedProduct.title">
        <h3>Product: {{ searchedProduct.title }}</h3>
        <p>Brand: {{ searchedProduct.brand }}</p>
        <p>Description: {{ searchedProduct.description }}</p>
        <p>Type: {{ searchedProduct.category }}</p>
        <p>Price: ${{ searchedProduct.price }}</p><br>
        <button type="submit" @click="addToCart(searchedProduct)" class="cart">Add to cart</button><br>
        <h1>Total: ${{ totalPrice }}</h1>
      </div>
      <div v-else>
        <input type="text" id="input-search" placeholder="Find Something?" v-model="searchTerm">
        <button type="submit" @click="search">Find</button>
        <p>No product found</p>
      </div>
    </div>
  </div>
</template>

<script>
import { products } from './products';

export default {
  data() {
    return {
      products: products,
      searchTerm: '',
      searchedProduct: null,
      totalPrice: 0
    };
  },
  methods: {
    search() {
      const foundProduct = this.products.find(product => product.title.toLowerCase().includes(this.searchTerm.toLowerCase()));
      if (foundProduct) {
        this.searchedProduct = foundProduct;
      } else {
        this.searchedProduct = null;
      }
    },
    addToCart(product) {
      this.totalPrice += product.price;
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@300;400;500;600;700&display=swap');
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Oswald', sans-serif;
}

body{
  background-color: #f8f8f8;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.card {
  width: 90%;
  max-width: 500px;
  border-radius: 15px;
  box-shadow: 0 8px 10px rgba(0, 0, 0, 0.1);
  padding: 10px;
  text-align: center;
}
.input-search{
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}
input[type="text"] {
  flex: 1;
  height: 40px;
  padding: 0 10px;
  border: solid 1px #ccc;
  border-radius: 5px;
  font-size: 16px;
  outline: none;
}
img {
  width: 80%;
  max-width: 300px;
  height: auto;
  border-radius: 10px;
}
button {
  height: 40px;
  padding: 0 20px;
  margin-left: 10px;
  border: none;
  border-radius: 5px;
  background-color: #ee4d2d;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}
button:hover {
  background-color: #f33f20;
}
h3 {
  margin-top: 10px;
  font-size: 24px;
}
p {
  margin: 5px 0;
  font-size: 18px;
  text-align: center;
}
button.add-to-cart {
  margin-top: 20px;
  width: 100%;
  height: 40px;
  border: none;
  border-radius: 5px;
  background-color: #ee4d2d;
  color: #fff;
  font-size: 18px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button.add-to-cart:hover {
  background-color: #f33f20;
}

</style>


