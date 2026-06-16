```vue
<template>
  <div class="login-container">

    <div class="login-card">

      <h1>SITTA</h1>
      <p>Sistem Informasi Tracking dan Tata Kelola Bahan Ajar</p>

      <form @submit.prevent="login">

        <div class="form-group">
          <label>Username</label>

          <input
            v-model="username"
            type="text"
            placeholder="Masukkan Username"
            required
          />
        </div>

        <div class="form-group">
          <label>Password</label>

          <input
            v-model="password"
            type="password"
            placeholder="Masukkan Password"
            required
          />
        </div>

        <button
          type="submit"
          class="login-button"
        >
          Login
        </button>

        <p
          v-if="errorMessage"
          class="error-message"
        >
          {{ errorMessage }}
        </p>

      </form>

    </div>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()

const username = ref('')
const password = ref('')
const errorMessage = ref('')

function login() {

  if (
    username.value === 'admin' &&
    password.value === 'admin123'
  ) {

    localStorage.setItem(
      'namaUser',
      username.value
    )

    router.push('/dashboard')

  } else {

    errorMessage.value =
      'Username atau Password salah!'

  }
}
</script>

<style scoped>
.login-container {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background: #f4f6f9;
}

.login-card {
  width: 400px;
  padding: 30px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0,0,0,.1);
}

.login-card h1 {
  text-align: center;
  margin-bottom: 10px;
  color: #003366;
}

.login-card p {
  text-align: center;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

.form-group label {
  display: block;
  margin-bottom: 5px;
}

.form-group input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}

.login-button {
  width: 100%;
  padding: 12px;
  border: none;
  background: #003366;
  color: white;
  border-radius: 5px;
  cursor: pointer;
}

.login-button:hover {
  background: #004a99;
}

.error-message {
  color: red;
  margin-top: 10px;
  text-align: center;
}
</style>
```
