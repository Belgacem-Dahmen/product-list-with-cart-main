<script setup>
import ProductList from './components/ProductList.vue';
import Cart from './components/Cart.vue';
import products from '../data.json'

</script>

<template>
   <ProductList :products="products" />
   <Cart />
</template>
<style>
   
</style>

