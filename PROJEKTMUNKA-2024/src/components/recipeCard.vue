<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  title: String,
  description: String,
  imageSrc: String,
  category: String
})
</script>

<template>
  <div class="card recipe-card">
    <img :src="imageSrc" :alt="title" class="card-img-top" />
    <div class="card-body">
      <h5 class="card-title">{{ props.title }}</h5>
      <p class="card-text">{{ props.description }}</p>
      <span class="badge bg-info text-dark">{{ props.category }}</span>
    </div>
  </div>
</template>

<style scoped>
.recipe-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
}

.recipe-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.card-img-top {
  width: 416px; 
  height: 200px; 
  object-fit: cover;
}
</style>