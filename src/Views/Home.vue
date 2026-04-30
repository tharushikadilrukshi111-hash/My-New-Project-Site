<template>
 
<section class="hero-pro">
<img 
  src="https://images.unsplash.com/photo-1607082348824-0a96f2a4b9da?q=80&w=1600&auto=format&fit=crop" 
  class="hero-bg" 
/>
    
    <div class="hero-overlay">
      <h1>Snappick Market</h1>
      <p>Find the best deals on trending products</p>
      <button class="btn btn-primary small-btn" @click="$emit('goShop')">Shop Now</button>
    </div>
</section>

   
    <div class="home-section">
       <h2 class="section-title">✨ Why Choose Us</h2>
    <div class="features">
    <div class="feature-card">🚚 Fast Delivery</div>
    <div class="feature-card">💳 Secure Payments</div>
    <div class="feature-card">⭐ Top Quality</div>
    <div class="feature-card">🔄 Easy Returns</div>
    </div>
    </div>

<div class="promo-banner">
  <h2>🔥 Mega Sale</h2>
  <p>Up to 50% OFF on selected items</p>
  <button class="btn btn-primary" @click="page='shop'">
    Shop Now
  </button>
</div>

<div class="testimonials">
  <h2>💬 What Customers Say</h2>

  <div class="testimonial-grid">
    <div class="testimonial-card">"Amazing quality!" ⭐⭐⭐⭐⭐</div>
    <div class="testimonial-card">"Fast delivery!" ⭐⭐⭐⭐⭐</div>
    <div class="testimonial-card">"Best prices!" ⭐⭐⭐⭐⭐</div>
  </div>
</div>

<div class="brand-section">
  <h2>Shop Anytime, Anywhere</h2>
  <p>Available on mobile & desktop</p>

<div class="brand-list">
  <div class="brand-section-item">🚚 Free Shipping</div>
  <div class="brand-section-item">🔒 Secure Payment</div>
  <div class="brand-section-item">📞 24/7 Support</div>
</div>
</div>

<div class="subscribe">
  <h2>Subscribe</h2>
  <div class="subscribe-box">
  <input placeholder="Enter your email"/>
  <button >Subscribe</button>
</div>
</div>
</template>

<script setup>
const emit = defineEmits(['goShop'])

const goShop = () => {
  emit('goShop')
}
</script>


<style scoped>

.hero {
  text-align: center;
  color: white;
  padding: 100px 20px;
}

.hero h1 {
  font-size: 75px;
}

.hero p{
  font-size: 25px;
}
.hero-pro {
  position: relative;
  height: 600px;
  width:100%;
  margin: 20px auto;
  border-radius: 20px;
  overflow: hidden;
  max-width:100%;
}
.hero-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  filter: brightness(0.9);
  z-index: 1;
}
.hero-overlay {
  position: absolute;
  z-index: 2;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
 background: linear-gradient(
    to right,
     rgba(0,0,0,0.4),
    rgba(0,0,0,0.2)
    );
  

  display: flex;
  flex-direction: column;
  justify-content: center;
  padding: 40px;
  color: white;
}
.hero-overlay h1 {
  font-size: 75px;
}

.hero-overlay p {
  margin: 10px 0;
  font-size: 18px;
}

.home-section {
  padding: 60px 40px;
  max-width: 100%;
  width:100%;
  margin: auto;
  text-align: center;
}
.features {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px,1fr));
  gap: 20px;
   margin-top: 40px;
}

.feature-card {
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(10px);
  padding: 25px;
  border-radius: 15px;
  color: white;
  font-size: 16px;
  transition: 0.3s;
}

.feature-card:hover {
  transform: translateY(-5px);
  background: rgba(255,255,255,0.25);
}
.promo-banner {
  margin: 40px auto;
  padding: 40px;
  border-radius: 20px;
  max-width: 1000px;
  text-align: center;
  background: linear-gradient(135deg, #ff7a18, #ffb347);
  color: white;
}
.promo-banner h2 {
  font-size: 26px;
}

.promo-banner p {
  margin: 10px 0;
}
.btn-primary {
  background: linear-gradient(135deg, #ff7a18, #ffb347);
  color: white;
  border-radius:10px;
}

.btn-primary:hover {
  opacity: 0.9;
}
.testimonials {
  padding: 60px 40px;
   margin-top: 40px;
}

.testimonials h2 {
  color: white;
  margin-bottom: 30px;
  font-size: 26px;
}
.testimonial-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.testimonial-card {
  padding: 20px;
  border-radius: 16px;
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(10px);
  color: white;
  transition: 0.3s;
}

.testimonial-card:hover {
  transform: translateY(-5px);
  background: rgba(255,255,255,0.25);
}
.brand-section {
  text-align: center;
  padding: 60px 20px;
  color: white;
}

.brand-section h2 {
  font-size: 28px;
  margin-bottom: 10px;
}

.brand-section p {
  opacity: 0.8;
  margin-bottom: 30px;
}
.brand-list {
  display: flex;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
}
.brand-section-item {
  padding: 12px 20px;
  border-radius: 999px;
  background: rgba(255,255,255,0.15);
  backdrop-filter: blur(8px);
  transition: 0.3s;
}

.brand-section-item:hover {
  background: white;
  color: #667eea;
}
.subscribe {
  text-align: center;
  padding: 60px 20px;
  color: white;
    margin-top: 40px;
}

.subscribe-box {
  margin-top: 20px;
  display: flex;
  justify-content: center;
  gap: 10px;
}
.subscribe-box button {
  padding: 12px 25px;
  border-radius: 999px;
  border: none;
  background: linear-gradient(135deg, #ff7a18, #ffb347);
  color: white;
  cursor: pointer;
  transition: 0.3s;
}

.subscribe-box button:hover {
  transform: scale(1.05);
}
.subscribe-box input {
  padding: 12px 20px;
  border-radius: 999px;
  border: none;
  width: 250px;
  outline: none;
}
</style>