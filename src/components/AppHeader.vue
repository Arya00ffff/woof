<template>
  <header class="app-header">
    <div class="logo">
      <img src="../assets/icons/logo.png" alt="Company Logo" class="logo-img" />
    </div>
    <div class="search-bar">
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
import '../assets/header.css'

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
</script>
