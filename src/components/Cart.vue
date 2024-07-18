<template>
    <div class="cart">
        <h3> Your Cart ( 0 )</h3>
        <div class="cart-empty">
            <img src="../assets/images/illustration-empty-cart.svg" alt="">
            <p>your added items will appear here</p>
        </div>
    </div>
</template>

<script setup>

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
</style>