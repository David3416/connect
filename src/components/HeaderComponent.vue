<script setup>
// import { ref } from 'vue'
import { reactive, computed } from 'vue'

const user = reactive({
  firstName: 'Alex',
  lastName: 'Smith',
})
const fullName = computed(() => {
  return user.firstName + ' ' + user.lastName
})
</script>

<template>
  <header class="header">
    <div class="header__wrapper">
      <input id="first-name" v-model="firstName" />
      <input id="last-name" v-model="LastName" />

      <label for="full-name">{{ fullName }}</label>
    </div>
  </header>
</template>
<style></style>
