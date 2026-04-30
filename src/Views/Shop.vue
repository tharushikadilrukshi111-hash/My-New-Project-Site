<template>

<div class="section-title">
  <h2> 🛍️ All Products</h2>
</div>

    <!-- CARDS -->
    <div  class="grid">
      <div v-for="p in filtered" :key="p.id" class="card">

        <img :src="p.thumbnail || 'https://picsum.photos/400/300'" @click="view(p)" style="cursor:pointer"/>

        <div class="card-body">
          <h3>{{ p.title }}</h3>
          <p>Rs.{{ p.price }}</p>

          <div class="actions">
            <button @click="view(p)">View</button>
            <button class="primary" @click="add(p)">Add to Cart</button>
          </div>
        </div>

      </div>
    </div>
    </template>

    <script setup lang="ts">
import { computed } from "vue"

const props = defineProps({
  products: Array,
  search: String
})

const filtered = computed(() =>
  props.products.filter(p =>
    p.title.toLowerCase().includes(props.search.toLowerCase())
  )
)
</script>


    <style scoped>
    .section-title h2 {
     font-size: 22px;
     }
    .section-title {
         padding: 10px 40px;
      font-size: 28px;
     margin-bottom: 30px;
     color: white;
     font-weight: 600;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px,1fr));
  gap: 20px;
  padding: 40px;
}
.card {
  backdrop-filter: blur(12px);
  background: rgba(255,255,255,0.15);
  border-radius: 20px;
  overflow: hidden;
  color: white;
  transition: 0.3s;
}

.card:hover {
  transform: translateY(-10px) scale(1.03);
}

.card img {
  width: 100%;
  height: 180px;
  object-fit: cover;
}

.card-body {
  padding: 15px;
}
.dark .card {
  background: rgba(255, 255, 255, 0.05);
  color: white;
}
.actions {
  display: flex;
  gap: 10px;
  margin-top: 10px;
}
</style>