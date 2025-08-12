<template>
  <div class="container mt-5 text-center">
    <h2>🏠 Chào mừng đến MyBlog</h2>
    <button @click="goToBlog" class="btn btn-success mt-3">Xem Blog</button>
  </div>
</template>

<script setup>
import { useRouter } from 'vue-router'
const router = useRouter()
const goToBlog = () => {
  router.push({ name: 'BlogList' })
}
</script>
