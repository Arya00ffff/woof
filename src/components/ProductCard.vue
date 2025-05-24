<template>
  <div class="product-card">
    <div class="product-image-wrapper">
      <img :src="product.image" :alt="product.name" class="product-image" />
    </div>
    <div class="product-info">
      <h3 class="product-name">{{ product.name }}</h3>
      <p :class="['product-status', { 'out-of-stock': product.status === 'Out of Stock' }]">
        {{ product.status }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'
import '../assets/products.css'

defineProps({
  product: {
    type: Object,
    required: true,
  },
})
</script>
