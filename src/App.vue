<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import 'bootstrap/dist/css/bootstrap.css'
import UserModal from './views/UserModal.vue' 

const router = useRouter()
const showUserModal = ref(false)

const handleLogout = () => {
  logoutUser()
  router.push({ name: 'Home' })
}

const openUserModal = () => {
  showUserModal.value = true
}
const closeUserModal = () => {
  showUserModal.value = false
}
</script>

<template>
  <div id="app">
    <!-- 🔷 Header -->
    <header class="bg-primary text-white py-3 shadow-sm">
      <div class="container d-flex justify-content-between align-items-center">
        <h1 class="h4 mb-0">🏠 <span class="fw-light">MyBlog</span></h1>
        <nav class="d-flex flex-wrap gap-2">
          <router-link to="/" class="btn btn-outline-light">🏠 Trang chủ</router-link>
          <router-link to="/blog" class="btn btn-outline-light">📚 Blog</router-link>
          <router-link to="/dashboard" class="btn btn-outline-light">📝 Đăng Bài Viết</router-link>
          <router-link to="/profile" class="btn btn-outline-light">👤 Hồ sơ</router-link>
          <button class="btn btn-light" @click="openUserModal">🔐 Tài Khoản</button>
        </nav>
      </div>
    </header>

    <!-- 🔷 Nội dung -->
    <main class="container py-4">
      <router-view />
    </main>

    <!-- 🔷 Modal đăng nhập/đăng ký -->
    <UserModal :showModal="showUserModal" @close="closeUserModal" />

    <!-- 🔷 Footer -->
    <footer class="bg-dark text-white pt-4 mt-5">
      <div class="container">
        <div class="row">
          <!-- Giới thiệu -->
          <div class="col-md-4 mb-3">
            <h5>📢 Giới thiệu</h5>
            <p>Chúng tôi là nền tảng chia sẻ bài viết, thông tin hữu ích về giáo dục, công nghệ và đời sống. Mọi nội dung đều được kiểm duyệt để đảm bảo tính chính xác và hữu ích.</p>
          </div>

          <!-- Liên hệ -->
          <div class="col-md-4 mb-3">
            <h5>📞 Liên hệ</h5>
            <ul class="list-unstyled">
              <li>✉️ Email: CongViet47@gmail.com</li>
              <li>📱 Hotline: 0123 456 789</li>
              <li>📍 Địa chỉ: FPT POLYTECHNIC, TP.HCM</li>
            </ul>
          </div>

          <!-- Mạng xã hội -->
          <div class="col-md-4 mb-3">
            <h5>🌐 Theo dõi chúng tôi</h5>
            <div class="d-flex gap-3">
              <a href="#" class="text-white text-decoration-none">📘 Facebook</a>
              <a href="#" class="text-white text-decoration-none">🐦 Twitter</a>
              <a href="#" class="text-white text-decoration-none">▶️ YouTube</a>
              <a href="#" class="text-white text-decoration-none">📸 Instagram</a>
            </div>
          </div>
        </div>

        <hr class="bg-white">
        <p class="text-center mb-0">&copy; 2025 Báo Online. Bản quyền được bảo hộ.</p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
nav .router-link-active {
  font-weight: bold;
  text-decoration: underline;
}

nav .router-link-exact-active {
  color: #ffc107;
}

header {
  border-bottom: 1px solid rgba(255, 255, 255, 0.2);
}

footer {
  opacity: 0.8;
}
</style>
