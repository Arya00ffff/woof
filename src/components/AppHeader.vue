<template>
  <header class="app-header">
    <div class="logo">
      <img src="../assets/icons/logo.png" alt="Company Logo" class="logo-img" />
    </div>
    <div class="search-bar" :style="{ display: isHome ? 'flex' : 'none' }">
      <input
        type="text"
        placeholder="Search products by name..."
        :value="searchTerm"
        @input="onInput"
      />
    </div>
    <div class="user-area">
      <button class="user-icon">👤</button>
    </div>
  </header>
</template>

<script setup>
import { computed } from 'vue'
import { useRoute } from 'vue-router'
import '../assets/header.css'

const route = useRoute()
defineProps({
  searchTerm: {
    type: String,
    default: '',
  },
})
const emit = defineEmits(['update:searchTerm'])

function onInput(e) {
  emit('update:searchTerm', e.target.value)
}
const isHome = computed(() => route.path === '/')
</script>
