<template>
  <div class="container mt-5">
    <h2>📝 Danh sách bài viết</h2>
    <ul class="list-group mt-3">
      <li v-for="post in posts" :key="post.id" class="list-group-item d-flex justify-content-between align-items-center">
        {{ post.title }}
        <router-link :to="`/blog/${post.id}`" class="btn btn-sm btn-outline-primary">Xem</router-link>
      </li>
    </ul>
  </div>
</template>

<script setup>
const posts = [
  { id: 1, title: 'Giới thiệu về Vue.js' },
  { id: 2, title: 'Hướng dẫn sử dụng Vue Router' },
  { id: 3, title: 'Quản lý trạng thái với Pinia' },
]
</script>
