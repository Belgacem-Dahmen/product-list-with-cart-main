<script setup>
import ProductList from './components/ProductList.vue';
import Cart from './components/Cart.vue';
import products from '../data.json'
import { ref } from 'vue';
const cartData = ref([]);

const addArticle = (product) => {
      cartData.value.push(product);
    };


</script>

<template>
   <ProductList :products="products" :cartData="cartData" :addArticle="addArticle" />
   <Cart :cartData='cartData' />
</template>
<style></style>

