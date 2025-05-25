<template>
  <div id="app">
    <Header v-model:searchTerm="searchTerm" />

    <main class="main-content container">
      <div v-if="filteredProducts.length === 0" class="no-products-found">
        No products found matching "{{ searchTerm }}"
      </div>
      <div class="product-grid" v-else>
        <ProductCard
          v-for="product in filteredProducts"
          :key="product.id"
          :product="product"
          @view-details="openModal"
        />
      </div>
    </main>

    <ProductModal :isVisible="isModalVisible" :product="selectedProduct" @close="closeModal" />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import Header from '../components/AppHeader.vue'
import ProductCard from '../components/ProductCard.vue'
import ProductModal from '../components/ProductModal.vue'
import productsData from '../data/products.json'

const products = ref([])
const searchTerm = ref('')
const isModalVisible = ref(false)
const selectedProduct = ref(null)

onMounted(() => {
  products.value = productsData
})

const filteredProducts = computed(() => {
  if (!searchTerm.value) {
    return products.value
  }
  const searchLower = searchTerm.value.toLowerCase()
  return products.value.filter((product) => product.name.toLowerCase().includes(searchLower))
})

const openModal = (product) => {
  selectedProduct.value = product
  isModalVisible.value = true
}

const closeModal = () => {
  isModalVisible.value = false
  selectedProduct.value = null
}
</script>
