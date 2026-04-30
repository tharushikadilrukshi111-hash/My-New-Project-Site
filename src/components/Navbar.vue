<template>
  <header class="nav-glass">

    <input
      v-if="page==='home' || page==='shop'"
      :value="search"
      @input="updateSearch($event)"
      placeholder="Search"
      class="search"
    />

    <div class="nav-actions">

      <button class="btn" @click="$emit('changePage','home')">Home</button>
      <button class="btn" @click="$emit('changePage','shop')">Shop</button>
      <button class="btn" @click="$emit('changePage','login')">Login</button>
      <button class="btn" @click="$emit('changePage','signup')">Sign Up</button>

      <button @click="$emit('toggleDark')">
        {{ isDark ? "☀️" : "🌙" }}
      </button>

      <button class="btn btn-primary" @click="$emit('openCart')">
        🛒 {{ cartCount }}
      </button>

    </div>
  </header>
</template>

<script setup lang="ts">

const props = defineProps<{
  search: string
  page: string
  isDark: boolean
  cartCount: number
}>()

const emit = defineEmits([
  "updateSearch",
  "changePage",
  "toggleDark",
  "openCart"
])

const updateSearch = (e: Event) => {
  const target = e.target as HTMLInputElement
  emit("updateSearch", target.value)
}

</script>
<style>
.nav-glass {
  display: flex;
  justify-content: space-between;
  padding: 15px 30px;
  backdrop-filter: blur(10px);
  background: rgba(255,255,255,0.2);
  color: white;
  }
  .search {
  padding: 8px 15px;
  border-radius: 20px;
  border: none;
  font-size:20px;
}
.btn {
  padding: 8px 20px;
  border-radius: 9999px;
  border: none;
  background: rgba(255,255,255,0.25);
  color: white;
  cursor: pointer;
}
.btn-primary {
  background: linear-gradient(135deg, #ff7a18, #ffb347);
    color: white;
  border-radius:10px;
}
.dark .nav-glass {
  background: rgba(0, 0, 0, 0.4);
  color: white;
}
</style>