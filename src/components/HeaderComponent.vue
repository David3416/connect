<script setup>
import { ref, reactive, computed, watch, watchEffect } from 'vue'

// 1. Создай quantity с помощью ref()
const quantity = ref(1)
// 2. Создай product с помощью reactive()
const product = reactive({
  name: 'Ноутбук',
  price: 1200,
})
const totalPrice = computed(() => {
  return quantity.value * product.price
})
const searchQuery = ref('')

function increase() {
  quantity.value++
}
function decrease() {
  if (quantity.value > 1) {
    quantity.value--
  }
}
watch(quantity, (newValue, oldValue) => {
  console.log('Было:', oldValue)
  console.log('Стало:', newValue)
})
watchEffect(() => {
  console.log(product.name)
  console.log(product.price)
})
const isProductFound = computed(() => {
  return product.name.toLowerCase().includes(searchQuery.value.toLowerCase())
})
const discount = computed(() => {
  if (quantity.value > 9) {
    return 20
  } else if (quantity.value > 4) {
    return 15
  } else if (quantity.value > 2) {
    return 10
  } else return 0
})
const finalPrice = computed(() => {
  return totalPrice.value * (1 - discount.value / 100)
})
const formattedPrice = computed(() => {
  return euroFormatter.format(finalPrice.value.toFixed(2))
})
const euroFormatter = new Intl.NumberFormat('de-DE', {
  style: 'currency',
  currency: 'EUR',
})
</script>

<template>
  <div>
    <h2>Корзина покупок</h2>
    <p>Товар: {{ product.name }}</p>
    <p>Цена: {{ product.price }} €</p>
    <p>
      Количество:
      <input type="number" v-model.number="quantity" min="1" />
    </p>
    <button @click="increase">+</button>
    <button @click="decrease" :disabled="quantity <= 1">-</button>
    <p>Итого: {{ totalPrice }} €</p>
    <input type="text" v-model="searchQuery" />
    <p v-if="isProductFound">Товар найден</p>
    <p v-else>Товар не найден</p>
    <p>Размер скидки: {{ discount }}</p>
    <p>Итоговая стоимость: {{ formattedPrice }}</p>
  </div>
</template>
<style></style>
