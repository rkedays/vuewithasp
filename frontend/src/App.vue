<template>
  <div class="app">
    <h1>Weather Forecast</h1>
    <ul v-if="forecasts.length">
      <li v-for="(item, index) in forecasts" :key="index">
        {{ item.date }} — {{ item.summary }} ({{ item.temperatureC }}°C)
      </li>
    </ul>
    <p v-else>Loading forecast data...</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const forecasts = ref([])

onMounted(async () => {
  try {
    const response = await fetch('/api/weatherforecast') // Proxy handles the real URL
    if (!response.ok) throw new Error('Network response was not OK')
    forecasts.value = await response.json()
  } catch (err) {
    console.error('API call failed:', err)
  }
})
</script>

<style scoped>
.app {
  font-family: sans-serif;
  padding: 1rem;
}
</style>
