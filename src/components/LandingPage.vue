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
      <div style="display: flex; justify-content: center">
        <button class="ShowAll" @click="toggleAllProducts">
          {{ showAllProducts ? 'Show Less' : 'Show All' }}
        </button>
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
import axios from 'axios'

const products = ref([])
const searchTerm = ref('')
const isModalVisible = ref(false)
const selectedProduct = ref(null)
const showAllProducts = ref(false)

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost:3000/products')
    products.value = response.data
  } catch (error) {
    console.error('Error fetching products:', error)
  }
})

const filteredProducts = computed(() => {
  let filtered = products.value
  if (searchTerm.value) {
    const searchLower = searchTerm.value.toLowerCase()
    filtered = filtered.filter((product) => product.name.toLowerCase().includes(searchLower))
  }
  return showAllProducts.value ? filtered : filtered.slice(0, 8)
})

const openModal = (product) => {
  selectedProduct.value = product
  isModalVisible.value = true
}

const closeModal = () => {
  isModalVisible.value = false
  selectedProduct.value = null
}

const toggleAllProducts = () => {
  showAllProducts.value = !showAllProducts.value
}
</script>

<style scoped>
.ShowAll {
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
  text-align: center;
  justify-content: center;
}
.ShowAll:hover {
  background-color: #0056b3;
  transform: scale(1.05);
}
</style>
