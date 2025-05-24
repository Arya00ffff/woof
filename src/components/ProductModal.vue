<template>
  <div class="modal-overlay" v-if="isVisible" @click.self="$emit('close')">
    <div class="modal-content">
      <button class="close-button" @click="$emit('close')">&times;</button>
      <div class="modal-body" v-if="product">
        <img :src="product.image" :alt="product.name" class="modal-product-image" />
        <h2>{{ product.name }}</h2>
        <p>
          <strong>Status:</strong>
          <span :class="{ 'out-of-stock': product.status === 'Out of Stock' }">
            {{ product.status }}
          </span>
        </p>
        <p><strong>Price:</strong> ${{ product.price.toFixed(2) }}</p>
        <p class="modal-description"><strong>Description:</strong> {{ product.description }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps({
  isVisible: Boolean,
  product: Object,
})

defineEmits(['close'])
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000;
}

.modal-content {
  background: white;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  max-width: 500px;
  width: 90%;
  position: relative;
  text-align: center;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.8rem;
  cursor: pointer;
  color: #555;
  padding: 5px 10px;
}

.close-button:hover {
  color: #333;
}

.modal-body {
  margin-top: 20px;
}

.modal-product-image {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.modal-body h2 {
  font-size: 1.8rem;
  margin-bottom: 10px;
  color: #333;
}

.modal-body p {
  font-size: 1.1rem;
  margin-bottom: 8px;
  color: #666;
}

.modal-description {
  margin-top: 15px;
  font-style: italic;
  line-height: 1.5;
}

.modal-body .out-of-stock {
  color: #e74c3c;
  font-weight: bold;
}
</style>
