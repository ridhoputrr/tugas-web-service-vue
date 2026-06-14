<template>
  <div class="container">
    <nav>
      <RouterLink to="/">Daftar User</RouterLink>
      <RouterLink to="/create">Tambah User</RouterLink>
    </nav>

    <RouterView />
  </div>
</template>

<style>
.container {
  max-width: 800px;
  margin: 30px auto;
  font-family: Arial, sans-serif;
}

nav {
  display: flex;
  gap: 12px;
  margin-bottom: 25px;
}

nav a {
  background: #2563eb;
  color: white;
  padding: 8px 14px;
  border-radius: 6px;
  text-decoration: none;
}
</style>