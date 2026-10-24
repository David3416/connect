<script setup>
import { ref } from 'vue'
import { reactive } from 'vue'

const user = reactive({
  name: 'Alex',
  age: 25,
  city: 'Riga',
})

const message = ref('Привет!')
//новое сообщение
const count = ref(0)

function chandge_name() {
  user.name = 'David'
}
function chandge_birthday() {
  user.age++
}
function changeMessage() {
  message.value = 'Новое сообщение'
}
function increment() {
  count.value++
}
function decrement() {
  count.value--
}
function reset() {
  count.value = 0
}
</script>

<template>
  <header class="header">
    <div class="header__wrapper">
      <div class="message">
        {{ message }}
        {{ count }}
        <button @click="changeMessage" class="btn">Изменить сообщение</button>
        <button @click="increment">+</button>
        <button @click="decrement" :disabled="count === 0">-</button>
        <button @click="reset">reset</button>
      </div>
      <div class="user">
        <div><label for="Name">Name</label></div>
        <div>{{ user.name }}</div>
      </div>

      <div class="user">
        <div><label for="Age">Age</label></div>
        {{ user.age }}
      </div>
      <div class="user">
        <div><label for="City">City</label></div>
        {{ user.city }}
      </div>
      <input v-model="name" placeholder="изменить город" />
      <button @click="chandge_name">Изменить имя</button>
      <button @click="chandge_birthday">День рождения</button>
    </div>
  </header>
</template>
<style>
.btn {
  margin-left: 30px;
}
.message {
  margin-bottom: 30px;
}
.user {
  display: flex;
}
.user div {
  margin-bottom: 10px;
  margin-left: 20px;
  margin-right: 20px;
}
.user input {
  margin-bottom: 10px;
  margin-left: 20px;
  margin-right: 20px;
}
button {
  margin-left: 20px;
}
</style>
