<script setup lang="ts">
import { ref, reactive, computed, watch } from 'vue';

const payment = reactive({
    name: 'Udemy',
    price: 1500,
    url: 'https://www.udemy.com/course/aws-linux-server-operation/?couponCode=ST13MT80425G2',
    urlName: 'AWS を用いたLinuxサーバー障害対応入門講座',
})

const inputName = (event: any) => {
    payment.name = event.target.value
}

// const inputPrice = (event: any) => {
//     payment.price = event.target.value
// }

const clear = () => {
    payment.name = ''
    payment.price = 0
}

const budget = 50000

// const priceLabel = computed(() => {
//     return payment.price > budget ? 'too expensive' : payment.price + ' yen'
// })

const priceLabel = ref<string>(payment.price + ' yen')

watch(() => payment.price, (newPrice) => {
    priceLabel.value = newPrice > budget ? 'too expensive' : newPrice.toString()
})

</script>

<template>
    <div class="container">
        <h1>リスト</h1>
        <input v-on:input="inputName" v-bind:value="payment.name" />
        <!-- <input @input="inputPrice" :value="payment.price" /> -->
        <input v-model="payment.price" />
        <button @click="clear">Clear</button>
        <div class="payment">
            <label>{{ payment.name }}</label>
            <p>{{ priceLabel }}</p>
            <a :href="payment.url" target="_blank">{{ payment.urlName }}</a>
        </div>
    </div>
</template>

<style scoped>
.container {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.payment {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 80px;
    width: 800px;
    background-color: aliceblue;
    margin: 8px;
    padding: 12px;
}

input {
    margin-bottom: 8px;
}

label {
    font-size: 20px;
    font-weight: bold;
}
</style>