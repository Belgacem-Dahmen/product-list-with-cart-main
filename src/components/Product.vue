<template>
    <div class="product">
        <div class="product__header">

            <picture class="product__header-img" :class="isSelected ? 'selected' : null" :onclick="toogleSelectedProduct">
                <source :srcset="getImageUrl(product.image.desktop)" media="(min-width: 1200px)">
                <source :srcset="getImageUrl(product.image.tablet)" media="(min-width: 768px)">
                <source :srcset="getImageUrl(product.image.mobile)" media="(min-width: 480px)">
                <img :src="getImageUrl(product.image.mobile)" :alt="product.name">
            </picture>
            <button v-if="!isSelected" class="product__header-btn" :onclick="handleClick"><img :src="cartIcon" alt="">Add To
                Cart</button>
            <button v-else class="product__header-btn orange"><img :src="decrementIcon" alt="" :onclick="handleUpdate">{{
                checkQuantity(product) }}
                <img :src="incrementIcon" alt="" :onclick="handleClick"></button>

        </div>
        <div class="product__infos">
            <p class="product__infos-category"> {{ product.category }}</p>
            <p class="product__infos-name"> {{ product.name }}</p>
            <p class="product__infos-price"> ${{ product.price }}</p>
        </div>



    </div>
</template>

<script setup>
import cartIcon from "@/assets/images/icon-add-to-cart.svg"
import incrementIcon from "@/assets/images/icon-increment-quantity.svg"
import decrementIcon from "@/assets/images/icon-decrement-quantity.svg"
import { ref } from "vue";

function getImageUrl(url) {
    return new URL(url, import.meta.url).href
}
const isSelected = ref(false)
const selectProduct = () => {
    isSelected.value = true
}

const toogleSelectedProduct = () => {
    isSelected.value = !isSelected.value
}
const { addArticle, product, updateQuantity, checkQuantity } = defineProps({
    product: {
        type: Object,
        default: () => { },
    },
    addArticle: Function,
    updateQuantity: Function,
    checkQuantity: Function
})


const handleClick = () => {
    selectProduct()
    addArticle(product)
}
const handleUpdate = () => {
    console.log(product);
    updateQuantity(product, "-")
}


</script>

<style scoped>
.product {
    display: flex;
    flex-direction: column;
    gap: 25px;

}

.product__header {
    position: relative;
}

.product__header-img {
    border-radius: 5px;
    overflow: hidden;

}

.selected {
    outline: 2px solid red;

}



.product__header-btn {

    align-items: center;
    justify-content: center;
    position: absolute;
    top: 100%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 25px;
    padding: 10px 20px;
    border: 1px solid gray;
    font-size: 14px;
    font-weight: var(--weight-semibold);
    background: white;
    min-width: fit-content;
    display: flex;
    gap: 10px;
}

.orange {
    background: rgb(236, 70, 10);
    justify-content: space-between;
}

@media screen and (min-width: 376px) {
    .product__header-btn {
        min-width: 60%;
    }

}
</style>