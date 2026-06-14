<template>
  <div>
    <h2>Detail Pengguna</h2>

    <p v-if="loading">Memuat detail user...</p>

    <div v-else-if="user" class="detail-card">
      <img :src="`https://i.pravatar.cc/150?img=${user.id}`" alt="avatar" />

      <h3>{{ user.name }}</h3>
      <p><b>Email:</b> {{ user.email }}</p>
      <p><b>Username:</b> {{ user.username }}</p>
      <p><b>Telepon:</b> {{ user.phone }}</p>
      <p><b>Website:</b> {{ user.website }}</p>
      <p><b>Perusahaan:</b> {{ user.company.name }}</p>

      <RouterLink to="/" class="back-btn">Kembali</RouterLink>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'

const route = useRoute()
const user = ref(null)
const loading = ref(true)

onMounted(async () => {
  try {
    const id = route.params.id
    const res = await axios.get(`https://jsonplaceholder.typicode.com/users/${id}`)
    user.value = res.data
  } catch (error) {
    console.error('Gagal mengambil detail user:', error)
  } finally {
    loading.value = false
  }
})
</script>

<style scoped>
.detail-card {
  border: 1px solid #ddd;
  padding: 25px;
  border-radius: 8px;
  text-align: center;
}

.detail-card img {
  width: 120px;
  height: 120px;
  border-radius: 50%;
}

.back-btn {
  display: inline-block;
  margin-top: 15px;
  background: #6b7280;
  color: white;
  padding: 8px 12px;
  border-radius: 6px;
  text-decoration: none;
}
</style>