<template>
  <div>
    <h2>Tambah Pengguna Baru</h2>

    <form @submit.prevent="createUser" class="form">
      <input v-model="name" placeholder="Nama" />
      <input v-model="email" placeholder="Email" />
      <input v-model="job" placeholder="Pekerjaan" />

      <button type="submit">Tambah</button>
    </form>

    <div v-if="response" class="success">
      <h3>Response API</h3>
      <p><b>ID:</b> {{ response.id }}</p>
      <p><b>Nama:</b> {{ response.name }}</p>
      <p><b>Email:</b> {{ response.email }}</p>
      <p><b>Pekerjaan:</b> {{ response.job }}</p>
    </div>

    <p v-if="error" class="error">{{ error }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'

const name = ref('')
const email = ref('')
const job = ref('')
const response = ref(null)
const error = ref('')

const createUser = async () => {
  error.value = ''
  response.value = null

  if (!name.value || !email.value || !job.value) {
    error.value = 'Nama, email, dan pekerjaan harus diisi.'
    return
  }

  try {
    const res = await axios.post('https://jsonplaceholder.typicode.com/users', {
      name: name.value,
      email: email.value,
      job: job.value
    })

    response.value = res.data
  } catch (err) {
    error.value = 'Gagal menambah pengguna.'
    console.error(err)
  }
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 400px;
}

input {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 6px;
}

button {
  background: #2563eb;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 6px;
  cursor: pointer;
}

.success {
  margin-top: 20px;
  background: #dcfce7;
  padding: 15px;
  border-radius: 8px;
}

.error {
  color: red;
  margin-top: 10px;
}
</style>