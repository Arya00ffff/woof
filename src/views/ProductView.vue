<script setup>
import { ref, computed, onMounted } from 'vue'
import { useRoute } from 'vue-router'
import productsData from '../data/products.json'

const route = useRoute()
const productId = computed(() => route.params.id)
const product = computed(() => productsData.find((p) => String(p.id) === String(productId.value)))
</script>

<template>
  <div v-if="product">
    <img :src="product.image" :alt="product.name" />
    <h2>{{ product.name }}</h2>
    <p>Status: {{ product.status }}</p>
    <p>Price: ${{ product.price.toFixed(2) }}</p>
    <p>{{ product.description }}</p>
  </div>
  <div v-else>
    <p>Product not found.</p>
  </div>
</template>
