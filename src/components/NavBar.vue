<template>
  <nav class="flex px-4 py-4 justify-center items-center bg-gray-800">
    <div class="text-white">
      <div class="animate__animated animate__fadeIn">
      {{ timeString }}
    </div>
    </div>
  </nav>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
const timeString = ref('')
const timeInterval = ref(null)

onMounted(() => {
  startClock()
})

// Before leave the page
onBeforeUnmount(() => {
  stopClock()
})

// Start Clock Method
const startClock = () => {
  // show time immediately
  timeString.value = new Date(Date.now()).toLocaleTimeString('el-GR')
  // show time every second after that
  timeInterval.value = setInterval(() => {
    timeString.value = new Date(Date.now()).toLocaleTimeString('el-GR')
  }, 1000) // every 1 Sec
}

// Stop Clock method
const stopClock = () => {
  clearInterval(timeInterval.value)
  timeInterval.value = null
}
</script>
