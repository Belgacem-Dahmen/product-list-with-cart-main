<template>
    <div class="productList">
        <div>
            <h1>Desserts</h1>
        </div>
        <div class="products__container">
            <div v-for="product in products" :key="product.id">
                <Product :product="product" :addArticle="addArticle" :updateQuantity="updateQuantity"/>
            </div>
        </div>

    </div>
</template>

<script setup>
import Product from './Product.vue';

const { addArticle , products, updateQuantity } = defineProps({
    products: Object,
    addArticle : Function,
    updateQuantity : Function
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

/* tablettes */
@media (min-width : 376px) and (max-width : 850px) {
    .productList {
        grid-column: span 3;
    }
    .products__container {
        display: grid;
        grid-template-columns: 1fr 1fr ;
        
    }
}

/* desktop */
@media screen and (min-width : 850px) {
    .productList {
        grid-column: span 3;
    }

    .products__container {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        
    }

}
</style>