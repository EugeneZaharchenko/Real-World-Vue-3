<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { inject } from 'vue'
import { useRouter } from 'vue-router'
const router = useRouter()
const GStore = inject('GStore')

const register = () => {
  GStore.flashMessage = 'U r nicely registered for event'
  setTimeout(() => {
    GStore.flashMessage = ''
  }, 3000)
  router.push({
    name: 'EventDetails',
  })
}
</script>
<template>
  <p>Register for the event here</p>
  <button @click="register">Register me</button>
</template>
