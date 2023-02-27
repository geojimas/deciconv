<script setup>
import NavBar from './components/NavBar.vue'
import ContentView from './components/ContentView.vue'
import FooterView from './components/FooterView.vue'
</script>

<template>
  <div class="flex flex-col h-screen justify-between">
    <NavBar />
    <ContentView />
    <FooterView />
  </div>
</template>
