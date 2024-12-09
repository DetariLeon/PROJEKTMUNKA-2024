  
<script setup>

</script>
<template>
    <div class="card recipe-card">
      <img :src="imageSrc" :alt="title" class="card-img-top" />
      <div class="card-body">
        <h5 class="card-title">{{ title }}</h5>
        <p class="card-text">{{ description }}</p>
        <span class="badge bg-primary">{{ category }}</span>
      </div>
    </div>
  </template>

  
  <style scoped>
 .recipe-card:hover .card-img-top {
  transform: scale(1.1);
  transition: transform 0.3s ease;
}
  </style>
  