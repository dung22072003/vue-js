<template>
  <div class="container mt-5">
    <h2>📝 {{ post?.title || 'Không tìm thấy bài viết' }}</h2>
    <p>{{ post?.content || 'Không có nội dung để hiển thị.' }}</p>
  </div>
</template>

<script setup>
import { useRoute } from 'vue-router'
const route = useRoute()
const postId = Number(route.params.id)

const posts = [
  { id: 1, title: 'Giới thiệu về Vue.js', content: 'Vue.js là một framework JavaScript linh hoạt...' },
  { id: 2, title: 'Hướng dẫn sử dụng Vue Router', content: 'Vue Router giúp quản lý điều hướng trong ứng dụng Vue...' },
  { id: 3, title: 'Quản lý trạng thái với Pinia', content: 'Pinia là thư viện quản lý trạng thái hiện đại cho Vue...' },
]

const post = posts.find(p => p.id === postId)
</script>
