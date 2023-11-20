<script setup>
import { RouterView } from 'vue-router'
import DexHeader from './components/DexHeader.vue';
import DexBanner from './components/DexBanner.vue';
</script>

<template>
  <DexHeader />
  <DexBanner />
  <RouterView />
</template>

<style scoped>

</style>
