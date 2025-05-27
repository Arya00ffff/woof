<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import productsData from '../data/products.json'
import AppHeader from '../components/AppHeader.vue'
import '../assets/products.css'

const route = useRoute()
const productId = computed(() => route.params.id)
const product = computed(() => productsData.find((p) => String(p.id) === String(productId.value)))
</script>
// I have no other way of rendering this
<template>
  <AppHeader />
  <div v-if="product">
    <img :src="product.image" :alt="product.name" style="max-height: 250px" />
    <h2>{{ product.name }}</h2>
    <p>Status: {{ product.status }}</p>
    <p>Price: ${{ product.price.toFixed(2) }}</p>
    <p>{{ product.description }}</p>
  </div>
  <div v-else>
    <p>Product not found.</p>
  </div>
</template>
