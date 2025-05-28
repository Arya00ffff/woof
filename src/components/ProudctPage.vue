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
  <div v-if="product">
    <img :src="product.image" :alt="product.name" style="max-height: 250px" />
    <h2>{{ product.name }}</h2>
    <p>Status: {{ product.status }}</p>
    <p>Price: ${{ product.price.toFixed(2) }}</p>
    <p>{{ product.description }}</p>
  </div>
  <div v-else>
    <PageNotFound />
  </div>
</template>
