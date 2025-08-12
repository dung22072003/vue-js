<template>
  <div class="container mt-5">
    <h2>🔐 Đăng nhập</h2>
    <form @submit.prevent="login" class="mt-3">
      <input v-model="username" placeholder="Tên đăng nhập" class="form-control mb-3" />
      <input type="password" v-model="password" placeholder="Mật khẩu" class="form-control mb-3" />
      <button class="btn btn-primary w-100">Đăng nhập</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import { authenticateUser } from '../router'

const username = ref('')
const password = ref('')
const router = useRouter()

const login = () => {
  if (username.value && password.value) {
    authenticateUser()
    router.push({ name: 'Dashboard' })
  } else {
    alert('Vui lòng nhập đầy đủ thông tin')
  }
}
</script>
