<template>
<div  class="auth">
  <div class="auth-wrapper">

    <!-- LEFT SIDE -->
    <div class="auth-left">
      <h1>Welcome Back 👋</h1>
      <p>Login to continue your learning journey</p>
    </div>

    <!-- RIGHT SIDE -->
    <div class="auth-card">
      <h2>Login</h2>
<input v-model="email" placeholder="Email"/>
<input v-model="password" type="password" placeholder="Password"/>
      
      <button @click="handleLogin">Login</button>

      <p class="link"  @click="$emit('go-signup')">
        Don't have an account? Sign up
      </p>
    </div>

  </div>
</div>
</template>

<script setup lang="ts">
import { ref } from "vue"

const emit = defineEmits(["login-success"])

const email = ref("")
const password = ref("")

const handleLogin = () => {
  if (email.value && password.value) {
    alert("Login successful!")
    emit("login-success")
  } else {
    alert("Fill all fields!")
  }
}
</script>
<style scoped>
.auth {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
.auth-wrapper {
  display: flex;
  width: 800px;
  height: 450px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 40px rgba(0,0,0,0.2);
  backdrop-filter: blur(10px);
}
.auth-left {
  flex: 1;
  background: linear-gradient(135deg, #667eea, #6ccef5);
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px;
}

.auth-left h1 {
  font-size: 32px;
}

.auth-left p {
  opacity: 0.9;
}
.auth-card {
  flex: 1;
  background: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px;
  gap: 12px;
}

.auth-card h2 {
  margin-bottom: 10px;
}

/* INPUTS */
.auth-card input {
  padding: 12px;
  border-radius: 10px;
  border: 1px solid #ddd;
  outline: none;
}

/* BUTTON */
.auth-card button {
  padding: 12px;
  border-radius: 10px;
  border: none;
  background: #ff7a18;
  color: white;
  cursor: pointer;
}
.dark .auth-card {
  background: #1e293b;
  color: white;
}

.dark .auth-card input {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}
.link {
  color: #667eea;
  cursor: pointer;
  font-size: 14px;
}
</style>
