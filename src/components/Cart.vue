<template>
    <div class="cart">
        <h3> Your Cart ({{ numberOfArticles }})</h3>
        <div v-if="isEmptyCart" class="cart-empty">
            <img src="../assets/images/illustration-empty-cart.svg" alt="">
            <p>your added items will appear here</p>
        </div>
        <div v-else class="cart-items">
            <div v-for="(article, key) in articles" :key="key">
                <div class="cart-item">

                    <div class="cart-item__infos">
                        <p class="cart-item__name">{{ article.name }}</p>
                        <p> <span>{{ article.quantity }}x</span> <span>@ ${{ article.price }}</span> <span>${{
                            article.quantity *
                            article.price }}</span></p>
                    </div>
                    <button class="cart-item__remove-btn">
                        <img :src="iconRemove" alt="">
                    </button>

                </div>
            </div>
            {{ totalPrice }}
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';
import iconRemove from "@/assets/images/icon-remove-item.svg"


const articles = computed(() => {
    const uniqueArticlesMap = new Map();
    cartData.forEach(article => {
        const key = JSON.stringify(article);
        if (uniqueArticlesMap.has(key)) {
            uniqueArticlesMap.get(key).quantity++;
        } else {
            uniqueArticlesMap.set(key, { ...article, quantity: 1 });

        }
    });

    return Array.from(uniqueArticlesMap.values());
});

const numberOfArticles = computed(() => {
    return cartData.length
})

const isEmptyCart = computed(() => {
    return cartData.length == 0 ? true : false
})

const totalPrice = computed(() => {
    return articles.value.reduce((sum, article) => {
        return sum + article.quantity * article.price;
    }, 0);
});


const { cartData } = defineProps({
    cartData: {
        type: Array,
        default: []
    }

})




</script>

<style scoped>
.cart {
    background: white;
    padding: 20px;
    border-radius: 10px;
}

.cart-empty {
    display: flex;
    flex-direction: column;
    gap: 15px;
    text-align: center;
    align-items: center;
    justify-content: center;
    height: min-content;
}
.cart-items {
    display: flex;
    margin-top: 25px;
    flex-direction: column;
    gap: 15px;

}
.cart-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.cart-item__remove-btn {
   border: 1px solid gray;
   background: transparent;
    border-radius: 50%;
    display: flex;align-items: center;padding: 2px;
    
    
}
</style>