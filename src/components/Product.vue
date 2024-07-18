<template>
    <div class="product" :onclick="selectProduct">
        <div class="product__header">
            <!-- <img class="product__header-img" :src="getImageUrl(product.image.mobile)" :alt="product.name" /> -->
            <picture class="product__header-img" :class="isSelected ? 'selected' : null">
                <source :srcset="getImageUrl(product.image.desktop)" media="(min-width: 1200px)">
                <source :srcset="getImageUrl(product.image.tablet)" media="(min-width: 768px)">
                <source :srcset="getImageUrl(product.image.mobile)" media="(min-width: 480px)">
                <img :src="getImageUrl(product.image.mobile)" :alt="product.name">
            </picture>
            <button class="product__header-btn">
                <img :src="cartIcon" alt="">
                Add To Cart</button>
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
import { ref } from "vue";
function getImageUrl(url) {
    return new URL(url, import.meta.url).href
}
const isSelected = ref(false)
const selectProduct = () => {
    isSelected.value = !isSelected.value
    console.log(isSelected);
}
const { product } = defineProps({
    product: Object
})




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
    display: flex;
    gap: 10px;
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
}

@media screen and (min-width: 376px) {
    .product__header-btn {
        min-width: 60%;
    }

}
</style>