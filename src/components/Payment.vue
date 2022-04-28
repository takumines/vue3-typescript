<script setup lang="ts">
import { ref, reactive, watch, toRefs } from 'vue';
const itemName1 = ref<string>('Desk')
const item2 = reactive({
  name: 'Bike',
  price: 20000
})
const budget = 50000

const url1 = 'https://www.amazon.co.jp/gp/product/479815072X/ref=ppx_yo_dt_b_asin_image_o01_s00?ie=UTF8&psc=1'
const buy = (itemName: string) => {
  alert('Are you sure to buy' + itemName + '?')
}

const clear = () => {
  item2.name = ''
  item2.price = 0
}

// const priceLabel = computed((): string => item2.price > budget ? 'too expensive' : item2.price + '円')
const priceLabel = ref<string>(item2.price + '円')
const { price } = toRefs(item2)
watch(price, () => {
  if (price.value > budget) {
    priceLabel.value = 'too expensive..'
  } else {
    priceLabel.value = price.value + '円'
  }
})

</script>

<template>
  <div class="container">
    <h1>最近の支出</h1>
    <input v-model="item2.name">
    <input v-model="item2.price">
    <button @click="clear">clear</button>
    <div class="payment">
      <label>{{ itemName1 }}</label>
      <label>{{ price1 }}円</label>
      <a :href="url1" target="_blank">bought at...</a>
      <button @click="buy(itemName1)">BUY</button>
    </div>
    <div class="payment">
      <label>{{ item2.name }}</label>
      <label>{{ priceLabel }}</label>
      <button @click="buy(item2.name)">BUY</button>
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
    width: 400px;
    background-color: aliceblue;
    margin-bottom: 8px;
  }
  input {
    margin-bottom: 8px;
  }
  label {
   font-size: 20px;
   font-weight: bold;
 }
</style>