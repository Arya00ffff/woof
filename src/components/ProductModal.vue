<template>
  <div v-if="isVisible" class="modal-overlay" @click.self="$emit('close')">
    <div class="modal-content">
      <button class="close-button" @click="$emit('close')">&times;</button>
      <div class="modal-body" v-if="product">
        <div class="modal-image-wrapper">
          <img :src="product.image" :alt="product.name" class="modal-image" />
        </div>
        <div class="modal-details">
          <h2>{{ product.name }}</h2>
          <p class="modal-status">
            Status:
            <span :class="{ 'out-of-stock': product.status === 'Out of Stock' }">
              {{ product.status }}
            </span>
          </p>
          <p class="modal-price">${{ product.price.toFixed(2) }}</p>
          <p class="modal-description">{{ product.description }}</p>
          <RouterLink :to="'/product/' + product.id">
            <button class="Go-to-page">Go to product page</button>
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import '../assets/modal.css'
import { RouterLink, useRoute } from 'vue-router'

defineProps({
  isVisible: Boolean,
  product: Object,
})

defineEmits(['close'])
</script>

<style scoped>
.Go-to-page {
  display: flex;
  margin: 20px auto;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-family: sans-serif;
  font-size: 20px;
  text-align: left;
  justify-content: left;
}
.Go-to-page:hover {
  background-color: #0056b3;
  transform: scale(1.05);
}
</style>
