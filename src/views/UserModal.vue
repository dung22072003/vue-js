<template>
  <Teleport to="body">
    <div class="modal fade" :class="{ show: showModal }" tabindex="-1" style="display: block;" v-if="showModal">
      <div class="modal-dialog modal-lg">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title">Đăng nhập / Đăng ký</h5>
            <button type="button" class="btn-close" @click="closeModal"></button>
          </div>
          <div class="modal-body">
            <!-- Tabs -->
            <ul class="nav nav-tabs" role="tablist">
              <li class="nav-item">
                <button class="nav-link" :class="{ active: activeTab === 'login' }" @click="activeTab = 'login'">Đăng Nhập</button>
              </li>
              <li class="nav-item">
                <button class="nav-link" :class="{ active: activeTab === 'register' }" @click="activeTab = 'register'">Đăng Ký</button>
              </li>
              <li class="nav-item">
                <button class="nav-link" :class="{ active: activeTab === 'forgot' }" @click="activeTab = 'forgot'">Quên mật khẩu</button>
              </li>
            </ul>

            <!-- Tab content -->
            <div class="tab-content pt-3">
              <!-- Login -->
              <div v-if="activeTab === 'login'">
                <form @submit.prevent="handleLogin">
                  <div class="mb-3">
                    <label>Email</label>
                    <input v-model="loginEmail" type="email" class="form-control" placeholder="Nhập email">
                  </div>
                  <div class="mb-3">
                    <label>Mật khẩu</label>
                    <input v-model="loginPassword" type="password" class="form-control" placeholder="Nhập mật khẩu">
                  </div>
                  <button type="submit" class="btn btn-success w-100">Đăng Nhập</button>
                  <div class="mt-2 text-center">
                    <a href="#" @click.prevent="activeTab = 'forgot'">Quên mật khẩu?</a>
                  </div>
                </form>
              </div>

              <!-- Register -->
              <div v-if="activeTab === 'register'">
                <form @submit.prevent="handleRegister">
                  <div class="mb-3">
                    <label>Họ và Tên</label>
                    <input v-model="registerName" type="text" class="form-control" placeholder="Nhập họ và tên">
                  </div>
                  <div class="mb-3">
                    <label>Email</label>
                    <input v-model="registerEmail" type="email" class="form-control" placeholder="Nhập email">
                  </div>
                  <div class="mb-3">
                    <label>Số điện thoại</label>
                    <input v-model="registerPhone" type="text" class="form-control" placeholder="Nhập số điện thoại">
                  </div>
                  <div class="mb-3">
                    <label>Mật khẩu</label>
                    <input v-model="registerPassword" type="password" class="form-control" placeholder="Nhập mật khẩu">
                  </div>
                  <div class="mb-3">
                    <label>Xác nhận mật khẩu</label>
                    <input v-model="confirmPassword" type="password" class="form-control" placeholder="Xác nhận mật khẩu">
                  </div>
                  <div class="mb-3">
                    <label>Giới tính</label><br>
                    <div class="form-check form-check-inline">
                      <input v-model="gender" type="radio" class="form-check-input" value="Nam" id="male">
                      <label class="form-check-label" for="male">Nam</label>
                    </div>
                    <div class="form-check form-check-inline">
                      <input v-model="gender" type="radio" class="form-check-input" value="Nữ" id="female">
                      <label class="form-check-label" for="female">Nữ</label>
                    </div>
                  </div>
                  <div class="mb-3">
                    <label>Ngôn ngữ</label>
                    <select v-model="language" class="form-select">
                      <option>Tiếng Việt</option>
                      <option>Tiếng Anh</option>
                    </select>
                  </div>
                  <div class="mb-3 form-check">
                    <input v-model="agreeTerms" type="checkbox" class="form-check-input" id="agree">
                    <label class="form-check-label" for="agree">Tôi đồng ý với các điều khoản và điều kiện</label>
                  </div>
                  <button type="submit" class="btn btn-primary w-100">Đăng Ký</button>
                </form>
              </div>

              <!-- Forgot password -->
              <div v-if="activeTab === 'forgot'">
                <form @submit.prevent="handleForgot">
                  <div class="mb-3">
                    <label>Email</label>
                    <input v-model="forgotEmail" type="email" class="form-control" placeholder="Nhập email">
                  </div>
                  <button type="submit" class="btn btn-warning w-100">Gửi yêu cầu</button>
                  <div class="mt-2 text-center">
                    <a href="#" @click.prevent="activeTab = 'login'">Quay lại đăng nhập</a>
                  </div>
                </form>
              </div>
            </div>
          </div>
          <div class="modal-footer">
            <button class="btn btn-secondary" @click="closeModal">Đóng</button>
          </div>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({ showModal: Boolean })
const emit = defineEmits(['close'])

const activeTab = ref('login')
const loginEmail = ref('')
const loginPassword = ref('')
const registerName = ref('')
const registerEmail = ref('')
const registerPhone = ref('')
const registerPassword = ref('')
const confirmPassword = ref('')
const gender = ref('')
const language = ref('Tiếng Việt')
const agreeTerms = ref(false)
const forgotEmail = ref('')

const closeModal = () => emit('close')

const handleLogin = () => {
  if (loginEmail.value && loginPassword.value) {
    localStorage.setItem('user', JSON.stringify({ name: registerName.value || 'Người dùng' }))
    emit('close')
    alert('Đăng nhập thành công!')
  } else {
    alert('Vui lòng nhập đầy đủ thông tin.')
  }
}

const handleRegister = () => {
  if (
    registerName.value &&
    registerEmail.value &&
    registerPhone.value &&
    registerPassword.value &&
    confirmPassword.value &&
    gender.value &&
    agreeTerms.value
  ) {
    if (registerPassword.value !== confirmPassword.value) {
      alert('Mật khẩu xác nhận không khớp.')
      return
    }
    alert('Đăng ký thành công (giả lập)')
    emit('close')
  } else {
    alert('Vui lòng điền đầy đủ thông tin và đồng ý điều khoản.')
  }
}

const handleForgot = () => {
  if (forgotEmail.value) {
    alert('Yêu cầu gửi lại mật khẩu đã được gửi (giả lập)')
    emit('close')
  } else {
    alert('Vui lòng nhập email.')
  }
}
</script>
