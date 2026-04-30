<template>
 <div :class="isDark ? 'dark' : ''" class="app">

    <!-- BACKGROUND -->
    <div class="bg-gradient"></div>

     <NavBar
      :search="search"
      :page="page"
      :isDark="isDark"
      :cartCount="cart.length"

      @updateSearch="search = $event"
      @changePage="page = $event"
      @toggleDark="isDark = !isDark"
      @openCart="showCart = true"
    />
   <Shop 
  v-if="page==='shop'"
  :products="products"
  :search="search"
  @add="add"
  @view="view"
/>

   <Home v-if="page==='home'" @goShop="page='shop'" />
   

  <!-- 🔥 PRODUCT DETAILS MODAL (UPGRADED) -->
<div v-if="selected" class="modal">
  <div class="modal-card">

  <!-- ❌ CLOSE BUTTON -->
    <button class="close-btn" @click="selected=null">✖</button>

    <!-- LEFT IMAGE -->
    <div class="modal-left">
      <img :src="selected.thumbnail" />
    </div>

    <!-- RIGHT DETAILS -->
    <div class="modal-right">
      <h2>{{ selected.title }}</h2>

      <p class="desc">{{ selected.description }}</p>

      <div class="price">Rs. {{ selected.price }}</div>

      <div class="rating">⭐⭐⭐⭐⭐ (4.8)</div>

      <!-- buttons -->
      <div class="modal-actions">
        <button class="btn btn-primary" @click="add(selected)">
          🛒 Add to Cart
        </button>

        <button class="btn" @click="selected=null">
          Close
        </button>
      </div>

    </div>

  </div>
</div>

    
    <!-- LOGIN -->
<div v-if="page==='login'" class="auth">
  <div class="auth-wrapper">

    <!-- LEFT SIDE -->
    <div class="auth-left">
      <h1>Welcome Back 👋</h1>
      <p>Login to continue your learning journey</p>
    </div>

    <!-- RIGHT SIDE -->
    <div class="auth-card">
      <h2>Login</h2>

      <input v-model="login.email" placeholder="Email"/>
      <input v-model="login.password" type="password" placeholder="Password"/>

      <button @click="handleLogin">Login</button>

      <p class="link" @click="page='signup'">
        Don't have an account? Sign up
      </p>
    </div>

  </div>
</div>

    <!-- SIGNUP -->
<div v-if="page==='signup'" class="auth">
  <div class="auth-wrapper">

    <div class="auth-left">
      <h1>Create Account 🚀</h1>
      <p>Join us and start learning today</p>
    </div>

    <div class="auth-card">
      <h2>Sign Up</h2>

      <input v-model="signup.name" placeholder="Name"/>
      <input v-model="signup.email" placeholder="Email"/>
      <input v-model="signup.password" type="password" placeholder="Password"/>

      <button @click="handleSignup">Create Account</button>

      <p class="link" @click="page='login'">
        Already have an account? Login
      </p>
    </div>

  </div>
</div>

   <!-- CART -->
<div v-if="showCart" class="cart-overlay">

  <div class="cart-panel">

    <h2>🛒 My Cart</h2>

    <!-- ITEMS -->
    <div v-if="cart.length === 0" class="empty">
      Your cart is empty
    </div>

    <div v-for="(c, index) in cart" :key="index" class="cart-item">

  <span>{{ c.title }}</span>
  <span>Rs. {{ c.price }}</span>

  <button class="remove-btn" @click="removeFromCart(index)">
    ❌
  </button>

</div>
    <!-- TOTAL -->
    <div class="cart-total">
      Total: <b>Rs. {{ total }}</b>
    </div>

    <!-- PAYMENT -->
    <h4>Payment Methods</h4>

    <button class="pay-btn">💳 Credit Card</button>
    <button class="pay-btn">📱 Mobile Payment</button>
    <button class="pay-btn">🏦 Bank Transfer</button>

    <!-- ACTIONS -->
    <button class="checkout">Checkout</button>
    <button class="back-btn" @click="showCart=false">⬅ Go Back</button>
   </div>
  </div>
<Footer/>
</div>
</template>

<script setup lang="ts">

import NavBar from "./components/NavBar.vue"
import Footer from "./components/Footer.vue"
import Home from "./Views/Home.vue"
import Shop from "./Views/Shop.vue"

import { ref, computed, onMounted } from "vue"
const heroImage = ref("https://images.unsplash.com/photo-1521335629791-ce4aec67dd53?q=80&w=1600&auto=format&fit=crop")
const search = ref("")
const selected = ref<Product | null>(null)
const cart = ref<Product[]>([])
const showCart = ref(false)
const isDark = ref(false)
const page = ref("home")
const removeFromCart = (index) => {
  cart.value.splice(index, 1)
}
type Product = {
  id: number
  title: string
  price: number
  description: string
  thumbnail: string
}
const products = ref<Product[]>([])

const login = ref({ email:"", password:"" })
const signup = ref({ name:"", email:"", password:"" })

/* FETCH + YOUR NAMES + PRICES */
onMounted(async () => {
  const res = await fetch("https://dummyjson.com/products?limit=30")
  const data = await res.json()
  products.value = data.products
})


/* FUNCTIONS */
const view = (p) => selected.value = p
const add = (p) => cart.value.push(p)

const total = computed(() =>
  cart.value.reduce((t, i) => t + i.price, 0)
)

/* AUTH */
const handleLogin = () => {
  if(login.value.email && login.value.password){
    alert("Login successful!")
    page.value = "home"
  } else {
    alert("Fill all fields!")
  }
}

const handleSignup = () => {
  if(signup.value.name && signup.value.email && signup.value.password){
    alert("Account created!")
    page.value = "home"
  } else {
    alert("Fill all fields!")
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: 'Poppins', sans-serif;
}

.bg-gradient {
  position: fixed;
  inset:0;
  width: 100vw;
  height: 100vh;
  background: 
    radial-gradient(circle at 10% 20%, #0f172a 0%, transparent 40%),
    radial-gradient(circle at 80% 30%, #1e3a8a 0%, transparent 45%),
    radial-gradient(circle at 50% 80%, #9333ea 0%, transparent 40%),
    linear-gradient(135deg, #0f172a, #111827);
  z-index: -1;

}

.logo {
  font-size: 22px;
  font-weight: bold;
  cursor:pointer;
}
html, body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
  overflow-x: hidden;
}
.app {
  width: 100vw;
  min-height: 100vh;
}
#app {
  width: 100vw;
  min-height: 100vh;
}

.actions {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}

.primary {
  background: #ff7a18;
  color: white;
  border:none;
  padding:5px 10px;
}

button {
  border-radius: 5000px;
}

/* 🌙 DARK MODE FIX */
.dark {
  background:
    radial-gradient(circle at 20% 20%, #1e293b 0%, transparent 40%),
    radial-gradient(circle at 80% 30%, #0f172a 0%, transparent 50%),
    radial-gradient(circle at 50% 80%, #312e81 0%, transparent 45%),
    linear-gradient(135deg, #020617, #0f172a);
}

/* cart */
.dark .cart {
  background: #1e293b;
  color: white;
}

/* auth boxes */
.dark .auth-card {
  background: #1e293b;
  color: white;
}

/* input fields */
.dark input {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}

/* 🌟 AUTH LAYOUT */
.auth {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

/* container split */
.auth-wrapper {
  display: flex;
  width: 800px;
  height: 450px;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 10px 40px rgba(0,0,0,0.2);
  backdrop-filter: blur(10px);
}

/* LEFT SIDE */
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

/* RIGHT SIDE FORM */
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

/* LINK */
.link {
  color: #667eea;
  cursor: pointer;
  font-size: 14px;
}

/* DARK MODE SUPPORT */
.dark .auth-card {
  background: #1e293b;
  color: white;
}

.dark .auth-card input {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}

/* CART OVERLAY */
.cart-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.6);
  display: flex;
  justify-content: flex-end;
}

/* CART PANEL */
.cart-panel {
  width: 450px;
  height: 100%;
  background: white;
  padding: 20px;
  overflow-y: auto;
  animation: slideIn 0.3s ease;
}

/* animation */
@keyframes slideIn {
  from { transform: translateX(100%); }
  to { transform: translateX(0); }
}

/* items */
.cart-item {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  border-bottom: 1px solid #eee;
}

/* total */
.cart-total {
  margin-top: 15px;
  font-size: 18px;
}

/* payment buttons */
.pay-btn {
  width: 100%;
  padding: 10px;
  margin-top: 8px;
  border: none;
  border-radius: 10px;
  background: #f1f1f1;
  cursor: pointer;
}

.pay-btn:hover {
  background: #ddd;
}

/* checkout */
.checkout {
  width: 100%;
  margin-top: 15px;
  padding: 12px;
  background: green;
  color: white;
  border: none;
  border-radius: 10px;
}

/* back button */
.back-btn {
  width: 100%;
  margin-top: 10px;
  padding: 12px;
  background: #ff7a18;
  color: white;
  border: none;
  border-radius: 10px;
}

/* empty cart */
.empty {
  text-align: center;
  color: gray;
  padding: 20px;
}

/* DARK MODE */
.dark .cart-panel {
  background: #1e293b;
  color: white;
}

.dark .pay-btn {
  background: #0f172a;
  color: white;
}

.dark .pay-btn:hover {
  background: #334155;
}

.home-btn {
  padding: 8px 20px;
  border-radius: 9999px; /* makes oval */
  border: none;
  background: rgba(255,255,255,0.3);
  color: white;
  font-weight: bold;
  cursor: pointer;
  backdrop-filter: blur(8px);
  transition: 0.3s;
}

/* hover effect */
.home-btn:hover {
  background: white;
  color: #667eea;
}

.dark .home-btn {
  background: rgba(0,0,0,0.4);
  color: white;
}

.dark .home-btn:hover {
  background: white;
  color: black;
}

.btn {
  padding: 8px 20px;
  border-radius: 9999px; /* oval shape */
  border: none;
  background: rgba(255,255,255,0.25);
  color: white;
  font-weight: 500;
  cursor: pointer;
  backdrop-filter: blur(8px);
  transition: 0.3s;
   font-size: 16px;
}
.small-btn {
  padding: 15px 2px;
  font-size:20px;
}

/* hover */
.btn:hover {
  background: white;
  color: #667eea;
}

/* primary button (important actions) */
.btn-primary {
  background: linear-gradient(135deg, #ff7a18, #ffb347);
  color: white;
  border-radius:10px;
}

.btn-primary:hover {
  opacity: 0.9;
}

.dark .btn {
  background: rgba(0,0,0,0.4);
  color: white;
}

.dark .btn:hover {
  background: white;
  color: black;
}

/* 🔥 CATEGORIES */
.categories {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px,1fr));
  gap: 20px;
  padding: 20px 40px;
}

.cat-card {
  background: rgba(255,255,255,0.2);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  text-align: center;
  padding: 15px;
  cursor: pointer;
  transition: 0.3s;
}

.cat-card:hover {
  transform: translateY(-5px);
}

.cat-card img {
  width: 100%;
  height: 100px;
  object-fit: cover;
  border-radius: 15px;
}

.cat-card h3 {
  margin-top: 10px;
  color: white;
}

/* 🔥 CATEGORY BAR */
.category-bar {
  display: flex;
  gap: 20px;
  padding: 20px 40px;
  overflow-x: auto;
}

.category-item {
  min-width: 120px;
  text-align: center;
  cursor: pointer;
}

.category-item img {
  width: 100%;
  height: 80px;
  object-fit: cover;
  border-radius: 15px;
}

.category-item span {
  display: block;
  margin-top: 5px;
  color: white;
}

/* 🔥 SERVICES */
.services {
  display: flex;
  justify-content: center;
  gap: 30px;
  margin-top: 20px;
  flex-wrap: wrap;
}

.services div {
  background: rgba(255,255,255,0.15);
  padding: 15px 25px;
  border-radius: 30px;
  color: white;
}
.section {
  margin-top: 40px;
} 

/* 🔥 MODAL BACKGROUND */
.modal {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

/* 🔥 MODAL CARD */
.modal-card {
  display: flex;
  gap: 30px;
  width: 800px;
  max-width: 90%;
  padding: 25px;
  border-radius: 20px;
  background: white;
  animation: fadeIn 0.3s ease;
  position:relative;
}

/* animation */
@keyframes fadeIn {
  from { transform: scale(0.9); opacity: 0 }
  to { transform: scale(1); opacity: 1 }
}

/* LEFT IMAGE */
.modal-left img {
  width: 300px;
  height: 300px;
  object-fit: cover;
  border-radius: 15px;
}

/* RIGHT SIDE */
.modal-right {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

/* title */
.modal-right h2 {
  margin-bottom: 10px;
}

/* description */
.desc {
  font-size: 14px;
  opacity: 0.8;
  margin-bottom: 15px;
}

/* price */
.price {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #ff7a18;
}

/* rating */
.rating {
  margin-bottom: 20px;
  font-size: 14px;
}

/* buttons */
.modal-actions {
  display: flex;
  gap: 10px;
}

/* DARK MODE */
.dark .modal-card {
  background: #1e293b;
  color: white;
}

/* ❌ CLOSE BUTTON */
.close-btn {
  z-index:10;
  position: absolute;
  top: 15px;
  right: 20px;
  border: none;
  border-radius: 50%;
  background: rgba(0,0,0,0.6);
  color: white;
  font-size: 18px;
  width: 35px;
  height: 35px;
  border-radius: 50%;
  cursor: pointer;
  transition: 0.3s;
}

.remove-btn {
  background: red;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 10px;
  cursor: pointer;
}

</style>