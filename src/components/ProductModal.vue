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
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import '../assets/modal.css'

defineProps({
  isVisible: Boolean,
  product: Object,
})

defineEmits(['close'])
</script>
