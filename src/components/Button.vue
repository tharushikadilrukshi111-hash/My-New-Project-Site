<template>
  <button :class="['btn', variant]" @click="$emit('click')">
    <slot />
  </button>
</template>

<script setup>
defineProps({
  variant: {
    type: String,
    default: "primary"
  }
})

defineEmits(["click"])
</script>

<style scoped>
.btn {
  padding: 10px 18px;
  border-radius: 999px;
  border: none;
  cursor: pointer;
  font-weight: bold;
}

.primary {
  background: #ff7a18;
  color: white;
}

.btn:hover {
  background: white;
  color: #667eea;
}




.dark .btn {
  background: rgba(0,0,0,0.4);
  color: white;
}

.dark .btn:hover {
  background: white;
  color: black;
}

</style>