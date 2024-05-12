<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { onMounted, ref, computed } from 'vue'
import EventService from '@/services/EventService.js'
import { useRouter } from 'vue-router'

const router = useRouter()

const props = defineProps(['id'])

const id = computed(() => props.id)

const event = ref(null)
onMounted(() => {
  EventService.getEvent(id.value)
    .then((response) => {
      event.value = response.data
    })
    // eslint-disable-next-line no-unused-vars
    .catch((error) => {
      if (error.response && error.response.status == 404) {
        router.push({
          name: '404Resource',
          params: { resource: 'event' },
        })
      } else {
        router.push({ name: 'NetworkError' })
      }
    })
})
</script>
<template>
  <div v-if="event">
    <h1>{{ event.title }}</h1>
    <div id="nav">
      <router-link :to="{ name: 'EventDetails' }">Details</router-link>
      |
      <router-link :to="{ name: 'EventRegister' }">Register</router-link>
      |
      <router-link :to="{ name: 'EventEdit' }">Edit</router-link>
    </div>
    <router-view :event="event" />
  </div>
</template>
