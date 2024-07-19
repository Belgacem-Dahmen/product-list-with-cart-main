<script setup>
import ProductList from './components/ProductList.vue';
import Cart from './components/Cart.vue';
import products from '../data.json'
import { ref } from 'vue';

const cartData = ref([]);

const addArticle = (product) => {
   cartData.value.push(product);
};

const removeArticle = (product) =>  {
  cartData.value = cartData.value.filter(article => article.name !== product.name);
}
</script>

<template>
   <ProductList :products="products" :cartData="cartData" :addArticle="addArticle" />
   <Cart :cartData='cartData'  :removeArticle="removeArticle"/>
</template>
<style></style>

