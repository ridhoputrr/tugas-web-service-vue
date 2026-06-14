<template>
  <div>
    <h2>Daftar Pengguna</h2>

    <p v-if="loading">Memuat data...</p>

    <div v-else class="user-list">
      <div v-for="user in users" :key="user.id" class="card">
        <img :src="`https://i.pravatar.cc/150?img=${user.id}`" alt="avatar" />

        <div>
          <h3>{{ user.name }}</h3>
          <p>{{ user.email }}</p>

          <RouterLink :to="`/user/${user.id}`" class="detail-btn">
            Lihat Detail
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const users = ref([])
const loading = ref(true)

onMounted(async () => {
  try {
    const res = await axios.get('https://jsonplaceholder.typicode.com/users')
    users.value = res.data
  } catch (error) {
    console.error('Gagal mengambil data:', error)
  } finally {
    loading.value = false
  }
})
</script>

<style scoped>
.user-list {
  display: grid;
  gap: 15px;
}

.card {
  display: flex;
  align-items: center;
  gap: 15px;
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 8px;
}

.card img {
  width: 70px;
  height: 70px;
  border-radius: 50%;
}

.detail-btn {
  display: inline-block;
  margin-top: 8px;
  background: #16a34a;
  color: white;
  padding: 6px 10px;
  border-radius: 5px;
  text-decoration: none;
}
</style>