<script setup>
import { authStore } from '@/stores/auth'
import { onMounted, ref, watch } from 'vue'

const store = authStore()
const showForm = ref(false)
const usernameNode = ref(null)
const notice = ref("")
const username = ref("")
const password = ref("")

// Очищает нотацию.
function clearNotice() {
  notice.value = '';
}

// Обновление токенов.
function refreshTokens() {
  fetch(import.meta.env.VITE_REFRESH_URL).then((res) => {
    if (res.ok) {
      res.json().then((body) => {
        store.accessToken = body.access_token
      })
      return
    }
    store.accessToken = ''
    showForm.value = true
  })
}

// Перевод строки в бинарное состояние.
function toBinaryStr(str) {
  const encoder = new TextEncoder();
  const charCodes = encoder.encode(str);
  return String.fromCharCode(...charCodes);
}

// Авторизация.
function login() {
  fetch(import.meta.env.VITE_LOGIN_URL, {
    headers: {
      'Authorization': 'Basic ' + btoa(toBinaryStr(username.value + ":" + password.value))
    },
  }).then((res) => {
    res.json().then((body) => {
      if (res.ok) {
        store.accessToken = body.access_token
        showForm.value = false
        username.value = ''
        password.value = ''
        return
      }
      notice.value = body.error
      usernameNode.value.focus()
    })
  })
}

watch(() => store.accessToken, (value, prev) => {
  if (value.length === 0) {
    refreshTokens()
  }
})

onMounted(() => {
  refreshTokens()
})
</script>

<template>
  <div class="shadow" v-if="showForm">
    <form @submit.prevent>
      <div class="auth">
        <div class="row">
          <h1>Authentication</h1>
        </div>
        <div class="row">
          <input type="text" placeholder="username" autofocus
           ref="usernameNode" v-model="username" @keypress="clearNotice" />
        </div>
        <div class="row">
          <input type="password" placeholder="password"
            v-model="password" @keypress="clearNotice"/>
        </div>
        <div class="row">
          <button @click="login">Login</button>
          <div class="notice">{{ notice }}</div>
        </div>
      </div>
    </form>
  </div>
</template>

<style scoped>
.shadow {
  background: rgb(0 0 0 / 80%);
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  .auth {
    border-radius: 20px;
    margin: 20px;
    padding: 30px;
    width: 400px;
    background: white;
    .row {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 5px 0;
      width: 100%;
      h1 {
        font-size: 24px;
        font-weight: 300;
      }
      .notice {
        color: red;
      }
    }
  }
}
</style>
