<script setup>
defineProps({
  resource: {
    type: String,
    required: true,
    default: 'page',
  },
})
</script>

<template>
  <h1>Oopss!!</h1>
  <h3>The {{ resource }} you're looking for is not found</h3>
  <router-link :to="{ name: 'EventList' }"> Back to home page </router-link>
</template>
