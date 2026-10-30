<script setup>
import { ref } from 'vue'

const API_URL = 'http://127.0.0.1:5000'
const text = ref('')
const result = ref('')

async function sendData() {
  const response = await fetch(`${API_URL}/submit`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ text: text.value })
  })
  const data = await response.json()
  result.value = 'Ответ: ' + JSON.stringify(data)
}
</script>

<template>
  <h1>Frontend v1.0</h1>
  <input v-model="text" type="text" placeholder="Введите текст" />
  <button @click="sendData">Отправить</button>
  <p>{{ result }}</p>
</template>