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
   <Login 
  v-if="page === 'login'" 
  @login-success="page = 'home'"
   @go-signup="page = 'signup'"
/>

<Signup 
  v-if="page === 'signup'" 
  @go-login="page = 'login'"
/>

<Home 
  v-if="page === 'home'" 
  @goShop="page = 'shop'"
/>

<Shop 
  v-if="page === 'shop'"
  :products="products"
  :search="search"
  @add="add"
  @view="view"
/>

<ProductDetails 
  v-if="selected"
  :product="selected"
  @close="selected = null"
  @add="add"
/>
<Cart 
  v-if="showCart"
  :cart="cart"
  :total="total"
  @close="showCart = false"
  @remove="removeFromCart"
/>

<Footer/>
</div>
</template>

<script setup lang="ts">

import NavBar from "./components/NavBar.vue"
import Footer from "./components/Footer.vue"
import Home from "./Views/Home.vue"
import Shop from "./Views/Shop.vue"
import ProductDetails from "./Views/ProductDetails.vue"
import Login from "./Views/Login.vue"
import Signup from "./Views/SignUp.vue"
import Cart from "./Views/MyCart.vue"

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
const isAuthPage = computed(() =>
  page.value === "login" || page.value === "signup"
)
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

/* input fields */
.dark input {
  background: #0f172a;
  color: white;
  border: 1px solid #334155;
}

/* animation */
@keyframes slideIn {
  from { transform: translateX(100%); }
  to { transform: translateX(0); }
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


.dark .btn {
  background: rgba(0,0,0,0.4);
  color: white;
}

.dark .btn:hover {
  background: white;
  color: black;
}

/* animation */
@keyframes fadeIn {
  from { transform: scale(0.9); opacity: 0 }
  to { transform: scale(1); opacity: 1 }
}

/* description */
.desc {
  font-size: 14px;
  opacity: 0.8;
  margin-bottom: 15px;
}



</style>