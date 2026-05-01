<script setup>
import Card from "../components/Card.vue"

defineProps({
  products: Array
})

defineEmits(["add", "view"])
</script>

<template>
  <div class="grid">
    <Card
      v-for="p in products"
      :key="p.id"
      :product="p"
      @add="$emit('add', $event)"
      @view="$emit('view', $event)"
    />
  </div>
</template>

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px,1fr));
  gap: 20px;
  padding: 40px;
}
</style>
