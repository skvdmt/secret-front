<script setup>
import Auth from '@/components/Auth.vue';
import { authStore } from '@/stores/auth'
import Secret from '@/components/Secret.vue';
const store = authStore()
</script>

<template>
  <Auth/>
  <div v-if="store.accessToken.length > 0">
    <Secret/>
  </div>
</template>

<style scoped>
</style>
