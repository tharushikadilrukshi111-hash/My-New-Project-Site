<template>
  <!-- CART -->
<div class="cart-overlay">

  <div class="cart-panel">

    <h2>🛒 My Cart</h2>

    <!-- ITEMS -->
    <div v-if="cart.length === 0" class="empty">
      Your cart is empty
    </div>

    <div v-for="(c, index) in cart" :key="index" class="cart-item">

  <span>{{ c.title }}</span>
  <span>Rs. {{ c.price }}</span>

  <button class="remove-btn" @click="emit('remove', index)">
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
<button class="GoBack" @click="() => { console.log('clicked'); emit('close') }">
  ⬅ Go Back
</button>
  </div>  
  </div>
  </template>

  <script setup>
const props = defineProps({
  cart: Array,
  total: Number
})

const emit = defineEmits(["close", "remove"])
</script>

<style scoped>
.cart-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.6);
  display: flex;
  justify-content: flex-end;
   z-index: 9999;
}
.cart-panel {
  width: 450px;
  height: 100%;
  background: white;
  padding: 20px;
  overflow-y: auto;
  animation: slideIn 0.3s ease;
  
}
.cart-panel h2{
     font-weight: 900; 
  color: #111; 
    font-size: 29px;
}
.cart-panel h4{
     font-weight: 600; 
  color: #111; 
    font-size: 25px;
}
.dark .cart-panel {
  background: #1e293b;
  color: white;
}
.empty {
  text-align: center;
  color: gray;
  padding: 20px;
}
.cart-item {
  display: flex;
  justify-content: space-between;
  padding: 8px 0;
  font-weight: 600; 
  color: #111; 
    font-size: 15px;
  border-bottom: 1px solid #eee;
}
.remove-btn {
  background: red;
  color: white;
  border: none;
  padding: 5px 10px;
  border-radius: 10px;
  cursor: pointer;
}
.cart-total {
  margin-top: 15px;
  font-size: 18px;
   font-weight: 600; 
  color: #111; 
  
}
.pay-btn {
  width: 100%;
  padding: 10px;
  margin-top: 8px;
  border: none;
  border-radius: 10px;
  background: #f1f1f1;
  cursor: pointer;
     font-weight: 800; 
  color: #111; 
    font-size: 15px;

}

.pay-btn:hover {
  background: #ddd;
}
.dark .pay-btn {
  background: #0f172a;
  color: white;
}

.dark .pay-btn:hover {
  background: #334155;
}
.checkout {
  width: 100%;
  margin-top: 15px;
  padding: 12px;
  background: green;
  color: white;
  border: none;
  border-radius: 10px;
}
.back-btn {
  width: 100%;
  margin-top: 10px;
  padding: 12px;
  background: #ff7a18;
  color: white;
  border: none;
  border-radius: 10px;
}
.GoBack {
 padding: 14px 20px;
 font-size: 16px;
 border-radius: 18px;

}
</style>