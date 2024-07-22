<template>
    <div class="cart">
        <h3 class="cart__title"> Your Cart ({{ numberOfArticles }})</h3>
        <div v-if="isEmptyCart" class="cart-empty">
            <img src="../assets/images/illustration-empty-cart.svg" alt="">
            <p>your added items will appear here</p>
        </div>
        <div v-else class="cart-items">
            <div v-for="(article, key) in articles" :key="key">
                <div class="cart-item">
                    <div class="cart-item__infos">
                        <p class="cart-item__name">{{ article.name }}</p>
                        <p>
                            <span class="cart-item__quantity">{{ article.quantity }}x</span>
                            <span>@ ${{ article.price }}</span>
                            <span>${{ article.quantity * article.price }}</span>
                        </p>
                    </div>
                    <button class="cart-item__remove-btn" @click="handleRemove(article)">
                        <img :src="iconRemove" alt="">
                    </button>
                </div>
            </div>
            <div class="order-total">
                <p class="order-total__text">Order Total </p>
                <p class="order-total__value"> ${{ totalPrice }}</p>
            </div>
            <div class="order__delivery">
                <img class="order__delivery-icon" :src="neutralIcon" alt="">
                <p class="order__delivery-text">This is a <span class="bold">carbon-neutral</span> delivery</p>
            </div>
            <button class="order__delivery-confirmBtn" @click="handleConfirm">
                Confirm Order
            </button>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue';
import iconRemove from "@/assets/images/icon-remove-item.svg";
import neutralIcon from "@/assets/images/icon-carbon-neutral.svg";

const props = defineProps({
    cartData: {
        type: Array,
        default: () => []
    },
    removeArticle: {
        type: Function,
        required: true
    },
    showModal: Function
});


const articles = computed(() => {
    const uniqueArticlesMap = new Map();
    props.cartData.forEach(article => {
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
    return props.cartData.length;
});

const isEmptyCart = computed(() => {
    return props.cartData.length === 0;
});

const totalPrice = computed(() => {
    return articles.value.reduce((sum, article) => {
        return sum + article.quantity * article.price;
    }, 0);
});

const handleRemove = (product) => {
    props.removeArticle(product);
};

const handleConfirm = () => {
    props.showModal();

}

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

.cart__title {
    font-size: 1.5rem;
    color: rgb(216, 63, 7);

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
    border-bottom: 0.1px solid var(--rose-100);
    padding-bottom: 10px;
}

.cart-item__name {
    font-weight: var(--weight-bold);
    font-size: 14px;
    margin-bottom: 10px;
}

.cart-item__remove-btn {
    border: 1px solid gray;
    background: transparent;
    border-radius: 50%;
    display: flex;
    align-items: center;
    padding: 2px;


}

.cart-item__quantity {
    color: rgb(216, 63, 7);
    font-weight: var(--weight-bold);

}

.order-total {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-top: 25px;
    border-radius: 10px;
}

.order-total__value {
    font-size: 2rem;
    font-weight: var(--weight-bold);
}


.order__delivery {
    padding: 20px 15px;
    display: flex;
    font-size: 14px;
    gap: 10px;
    background: var(--rose-100);
}

.order__delivery-confirmBtn {
    background-color: rgb(216, 63, 7);
    border-radius: 45px;
    border: none;
    color: var(--rose-100);
    padding: 15px;
    font-weight: var(--weight-semi-bold);
}
</style>