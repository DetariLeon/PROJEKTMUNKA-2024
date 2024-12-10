<script setup>
import { ref, computed } from 'vue';
import RecipeCard from './components/RecipeCard.vue';
import { recipes } from './assets/dummyData';

const searchQuery = ref('');
const selectedDifficulty = ref('');
const selectedCookTime = ref('');

const filteredRecipes = computed(() => {
  return recipes.filter((recipe) => {
    const matchesSearch = recipe.name.toLowerCase().includes(searchQuery.value.toLowerCase());
    const matchesDifficulty = selectedDifficulty.value ? recipe.difficulty === selectedDifficulty.value : true;
    const matchesCookTime = selectedCookTime.value ? recipe.cookTime <= selectedCookTime.value : true;

    return matchesSearch && matchesDifficulty && matchesCookTime;
  });
});
</script>

<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container">
      <a class="navbar-brand" href="#">Receptkönyv</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#receptek">Receptek</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#ujReceptek">Új recept</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#kedvencek">Kedvencek</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div class="container my-3">
    <form class="row">
      <div class="col-md-6">
        <input type="text" class="form-control" placeholder="Keress receptet..." v-model="searchQuery" />
      </div>

      <div class="col-md-3">
        <select class="form-select" v-model="selectedDifficulty">
          <option value="">Minden nehézség</option>
          <option value="könnyű">Könnyű</option>
          <option value="közepes">Közepes</option>
          <option value="nehéz">Nehéz</option>
        </select>
      </div>

      <div class="col-md-3">
        <select class="form-select" v-model="selectedCookTime">
          <option value="">Elkészítési idő szerint</option>
          <option value="30">30 perc alatt</option>
          <option value="60">60 perc alatt</option>
          <option value="90">90 perc alatt</option>
          <option value="120">120 perc alatt</option>
        </select>
      </div>
    </form>
  </div>

  <div class="container my-4">
    <div class="row g-4">
      <div class="col-md-4" v-for="recipe in filteredRecipes" :key="recipe.id">
        <RecipeCard :title="recipe.name" :description="'Elkészítési idő: ' + recipe.cookTime + ' perc'"
          :category="'Nehézségi szint: ' + recipe.difficulty" :imageSrc="recipe.imageUrl" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.navbar-brand {
  font-weight: bold;
}

.nav-item .nav-link {
  text-transform: capitalize;
}
</style>
