<script setup>
import { ref } from 'vue'

const API_URL = import.meta.env.VITE_API_URL ?? 'http://127.0.0.1:5000'
const text = ref('')
const result = ref('')
const filter = ref('')
const output = ref('')

async function sendData() {
  const response = await fetch(`${API_URL}/submit`, {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({text: text.value})
  })
  const data = await response.json()
  result.value = 'Ответ: ' + JSON.stringify(data)
}

async function readData() {
  const response = await fetch(
      `${API_URL}/read?query=${encodeURIComponent(filter.value)}`
  )
  const data = await response.json()
  output.value = data.content
}
</script>

<template>
  <h1>Frontend v2.0</h1>

  <h2>Отправка данных</h2>
  <input v-model="text" type="text" placeholder="Введите текст"/>
  <button @click="sendData">Отправить</button>
  <p>{{ result }}</p>

  <hr/>

  <h2>Просмотр данных</h2>
  <input v-model="filter" type="text" placeholder="Фильтр (необязательно)"/>
  <button @click="readData">Показать данные</button>
  <br/>
  <textarea v-model="output" rows="6" cols="50" readonly></textarea>
</template>