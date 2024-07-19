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


const updateQuantity = (article , signe) => {

if (signe == "+") {
    article.quantity++
} else if (signe == "-") {
    article.quantity--
}
    

}
</script>

<template>
   <ProductList :products="products" :cartData="cartData" :addArticle="addArticle" :updateQuantity="updateQuantity" />
   <Cart :cartData='cartData'  :removeArticle="removeArticle" />
</template>
<style></style>

