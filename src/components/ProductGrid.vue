<template>
  <div class="product-grid">
    <ProductCard
      v-for="product in products"
      :key="product.id"
      :product="product"
      @click="handleProductClick(product)"
    />
    <p v-if="products.length === 0" class="no-products-message">
      No products found matching your search.
    </p>
  </div>
</template>

<script setup>
import ProductCard from './ProductCard.vue'

const emit = defineEmits(['open-modal'])

defineProps({
  products: {
    type: Array,
    required: true,
  },
})

function handleProductClick(product) {
  emit('open-modal', product)
}
</script>
