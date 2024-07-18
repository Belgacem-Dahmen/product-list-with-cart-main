<template>
    <div class="productList">
        <div>
            <h1>Desserts</h1>
        </div>
        <div class="products__container">
            <div v-for="product in products" :key="product.id">
                <Product :product="product" />
            </div>
        </div>

    </div>
</template>

<script setup>
import Product from './Product.vue';

const { products } = defineProps({
    products: Object
})
</script>

<style scoped>
h1 {
    margin-bottom: 50px;
}

.products__container {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

@media screen and (min-width : 376px) {
    .productList {
        grid-column: span 3;
    }

    .products__container {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;

    }

}
</style>