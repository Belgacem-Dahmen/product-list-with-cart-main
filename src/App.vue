<script setup>
import ProductList from './components/ProductList.vue';
import Cart from './components/Cart.vue';
import products from '../data.json'
import { ref } from 'vue';

const cartData = ref([]);

const addArticle = (product) => {
  cartData.value.push(product);

};

const removeArticle = (product) => {
  cartData.value = cartData.value.filter(article => article.name !== product.name);
}


const updateQuantity = (product) => {
  const index = cartData.value.findIndex(item => item.name === product.name);
  if (index !== -1) {
    cartData.value.splice(index, 1);
  }

};

const checkQuantity = (product) => {
  return cartData.value.filter(item => item.name === product.name).length;
}

</script>

<template>
  <ProductList :products="products" :cartData="cartData" :addArticle="addArticle" :updateQuantity="updateQuantity"
    :checkQuantity="checkQuantity" />
  <Cart :cartData='cartData' :removeArticle="removeArticle" />
</template>
<style></style>

