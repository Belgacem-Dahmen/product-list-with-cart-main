<template>
    <div v-if="show" id="overlay" class="overlay">
        <div class="modal">
            <img class="modal__succes-icon" :src="SuccessIcon" alt="">
            <h2 class="modal__title">Order Confirmed</h2>
            <p class="modal__text">We hope you enjoy your food</p>

            <div class="modal__items">
                <div class="modal__item" v-for="article in articles" :key="article.id">
                    <div class="modal__item-infos">
                        <div class="modal__item-infos-left">
                            <img class="modal__item-img" :src="resolveUrl(article.image.thumbnail)" alt="">
                            <div>
                                <p class="modal__item-name">{{ article.name }}</p>
                                <div class="modal__item--infos">
                                    <span class="modal-item__quantity">{{ article.quantity }}x</span>
                                    <span class="modal-item__uniquePrice">@ ${{ article.price }}</span>


                                </div>
                            </div>
                        </div>

                        <div>
                            <p><span class="modal-item__price">${{ article.quantity * article.price }}</span></p>

                        </div>
                    </div>

                </div>
                <div class="modal__order-infos">
                    <p>Order total</p>
                    <p class="modal__total-price"> ${{ totalPrice }}</p>
                </div>
            </div>
            <button class="order__delivery-confirmBtn" id="close-button" @click="handleClose">Start New Order</button>
        </div>
    </div>
</template>

<script setup>
import SuccessIcon from "@/assets/images/icon-order-confirmed.svg"
import { computed } from "vue";

const resolveUrl = (relativePath) => {
    return new URL(`../assets/images/${relativePath}`, import.meta.url).href;
};

const { cartData, show, closeModal,resetQuantity } = defineProps({
    cartData: {
        type: Array,
        default: () => []
    }, 
    show: Boolean,
    closeModal: Function,
    resetQuantity: Function
})


const handleClose = () => {
    resetQuantity()
    closeModal()
}



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

const totalPrice = computed(() => {
    return articles.value.reduce((sum, article) => {
        return sum + article.quantity * article.price;
    }, 0);
});
</script>

<style scoped>
.overlay {
    display: flex;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.6);

    justify-content: center;
    align-items: center;
}

.modal {
    background-color: white;
    padding: 40px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.9);
    text-align: left;
    min-width: 600px;
    max-height: 80vh;
    overflow-y: scroll;

}

.modal__items {
    background: var(--rose-100);
    padding: 20px;
    border-radius: 5px;
    display: flex;
    gap: 20px;
    flex-direction: column;

}

.modal__item {
    display: flex;
    gap: 20px;
    border-bottom: 1px solid rgba(238, 226, 226, 0.945);
    padding-bottom: 20px;

}

.modal__item-img {
    border-radius: 10px;
    max-width: 50px;
}

.modal__item-infos {
    display: flex;
    min-width: 100%;
    justify-content: space-between;
    align-items: center;


}

.modal__item-infos-left {
    display: flex;
    gap: 20px;
}

.modal-item__quantity {
    margin-right: 25px;
    font-weight: var(--weight-bold);
    color: rgb(180, 62, 19);

}

.modal-item__uniquePrice {
    color: var(--rose-500);
}

.modal-item__price {
    font-weight: var(--weight-bold);
    font-size: 1.25rem;
}

.modal__order-infos {
    display: flex;
    min-width: 100%;
    justify-content: space-between;
    align-items: center;
}

.modal__total-price {
    font-size: 1.5rem;
    font-weight: var(--weight-bold);
}

button {
    padding: 10px 20px;
    margin-top: 20px;
    cursor: pointer;
}

#open-button {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}

.order__delivery-confirmBtn {
    background-color: rgb(216, 63, 7);
    min-width: 100%;
    border-radius: 45px;
    border: none;
    color: var(--rose-100);
    padding: 15px;
    font-weight: var(--weight-semi-bold);

}

@media screen and (max-width:375px) {
    .overlay {
        display: flex;
        /* Hidden by default */
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, 0.6);
        /* Black background with opacity */
        justify-content: center;
        align-items: flex-end;
    }

    .modal {
        background-color: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.9);
        text-align: left;
        min-width: 100%;
        min-height: 90%;

    }
}
</style>