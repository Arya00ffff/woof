<script setup>
import { computed, onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'
import axios from 'axios'
import AppHeader from '../components/AppHeader.vue'
import '../assets/products.css'
import PageNotFound from './PageNotFound.vue'

const products = ref([])
onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:3000/products')
    products.value = response.data
  } catch (error) {
    console.error('Error fetching products:', error)
  }
})
const route = useRoute()
const productId = computed(() => route.params.id)
const product = computed(() => products.value.find((p) => String(p.id) === String(productId.value)))
</script>

<template>
  <AppHeader />
  <div class="product-detail-container" v-if="product">
    <div class="product-detail-card">
      <img :src="product.image" :alt="product.name" class="product-detail-image" />
      <div class="product-detail-info">
        <h2 class="product-detail-title">{{ product.name }}</h2>
        <p class="product-detail-status">
          Status:
          <span :class="{ 'out-of-stock': product.status === 'Out of Stock' }">
            {{ product.status }}
          </span>
        </p>
        <p class="product-detail-price">Price: ${{ product.price.toFixed(2) }}</p>
        <p class="product-detail-description">{{ product.description }}</p>
      </div>
    </div>
  </div>
  <div v-else>
    <PageNotFound />
  </div>
</template>
