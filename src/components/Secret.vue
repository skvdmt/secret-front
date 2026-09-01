<script setup>
import { authStore } from '@/stores/auth'
import {onMounted, ref} from "vue";

const store = authStore()
const secret = ref("")

// Получение секрета.
async function getSecret() {
  fetch(import.meta.env.VITE_SECRET_URL, {
    credentials: 'omit',
    headers: {
      'Authorization': `Bearer ${store.accessToken}`
    }
  }).then((res) => {
    res.json().then((body) => {
      if (res.ok) {
        secret.value = body.secret
        return
      }
    })
  })
}

// Разлогинивание.
function logout() {
  fetch(import.meta.env.VITE_LOGOUT_URL, {
    credentials: 'omit',
  }).then((res) => {
    res.json().then((body) => {
      if (res.ok) {
        store.accessToken = ''
        return
      }
    })
  })
}

onMounted(() => {
  getSecret()
})

</script>

<template>
  <div class="secret">
    <div class="card">
      <h1>{{ secret }}</h1>
    </div>
    <button class="logout" @click="logout">Logout</button>
  </div>
</template>

<style scoped>
.secret {
  width: 100%;
  height: 100vh;
  display: flex;
  gap: 10px;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  .card {
    max-width: 500px;
    margin: 20px;
    padding: 30px;
    border-radius: 20px;
    background-color: white;
    align-items: center;
    h1 {
      font-weight: normal;
    }
  }
}
</style>
