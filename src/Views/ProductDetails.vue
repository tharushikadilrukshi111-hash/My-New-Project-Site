<template>
<div  class="modal">
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
</template>

<script setup lang="ts">

const props = defineProps({
  product: Object
})

const emit = defineEmits(["close", "add"])

</script>

<style scoped>
.modal {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}
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
.dark .modal-card {
  background: #1e293b;
  color: white;
}
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
.modal-left img {
  width: 300px;
  height: 300px;
  object-fit: cover;
  border-radius: 15px;
}
.modal-right {
  flex: 1;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.modal-right h2 {
  margin-bottom: 10px;
}
.price {
  font-size: 22px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #ff7a18;
}
.rating {
  margin-bottom: 20px;
  font-size: 14px;
}
.modal-actions {
  display: flex;
  gap: 10px;
}
.btn-primary {
  background: linear-gradient(135deg, #ff7a18, #ffb347);
  color: white;
  border-radius:10px;
}

.btn-primary:hover {
  opacity: 0.9;
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
.desc {
  font-size: 14px;
  opacity: 0.8;
  margin-bottom: 15px;
}
</style>


