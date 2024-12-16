<script setup>
import { ref, computed } from 'vue';
import { recipes } from './assets/dummyData';

const searchQuery = ref('');
const selectedDifficulty = ref('');
const selectedCookTime = ref('');
const activeTab = ref('receptek');

const newRecipeName = ref('');
const newRecipeCookTime = ref('');
const newRecipeDifficulty = ref('');

const filteredRecipes = computed(() => {
  return recipes.filter((recipe) => {
    const matchesSearch = recipe.name.toLowerCase().includes(searchQuery.value.toLowerCase());
    const matchesDifficulty = selectedDifficulty.value ? recipe.difficulty === selectedDifficulty.value : true;
    const matchesCookTime = selectedCookTime.value ? recipe.cookTime <= selectedCookTime.value : true;

    return matchesSearch && matchesDifficulty && matchesCookTime;
  });
});

const addNewRecipe = () => {
  if (!newRecipeName.value || !newRecipeCookTime.value || !newRecipeDifficulty.value) {
    alert('Minden mezőt ki kell tölteni!');
    return;
  }

  recipes.push({
    id: Date.now(),
    name: newRecipeName.value,
    cookTime: parseInt(newRecipeCookTime.value),
    difficulty: newRecipeDifficulty.value,
    imageUrl: '' // Az új receptekhez nem adunk képet
  });

  newRecipeName.value = '';
  newRecipeCookTime.value = '';
  newRecipeDifficulty.value = '';
  alert('Új recept sikeresen hozzáadva!');
};
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
            <a class="nav-link active" :class="{ active: activeTab === 'receptek' }" @click="activeTab = 'receptek'" href="#">Receptek</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" :class="{ active: activeTab === 'ujReceptek' }" @click="activeTab = 'ujReceptek'" href="#">Új recept</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <div v-if="activeTab === 'receptek'" class="container my-4">
    <form class="row">
      <div class="col-md-6">
        <input type="text" class="form-control" placeholder="Keresés recept név alapján..." v-model="searchQuery" />
      </div>

      <div class="col-md-3">
        <select class="form-select" v-model="selectedDifficulty">
          <option value="">Nehézségi szint</option>
          <option value="könnyű">Könnyű</option>
          <option value="közepes">Közepes</option>
          <option value="nehéz">Nehéz</option>
        </select>
      </div>

      <div class="col-md-3">
        <select class="form-select" v-model="selectedCookTime">
          <option value="">Elkészítési idő</option>
          <option value="30">30 perc alatt</option>
          <option value="60">60 perc alatt</option>
          <option value="90">90 perc alatt</option>
          <option value="120">120 perc alatt</option>
        </select>
      </div>
    </form>

    <div class="row g-4 mt-3">
      <div class="col-md-4" v-for="recipe in filteredRecipes" :key="recipe.id">
        <div class="card h-100">
          <img :src="recipe.imageUrl" class="card-img-top" alt="recipe.name"
            style="height: 200px; object-fit: cover;" />
          <div class="card-body">
            <h5 class="card-title">{{ recipe.name }}</h5>
            <p class="card-text">
              Elkészítési idő: {{ recipe.cookTime }} perc
            </p>
            <p class="card-text" :class="{
              'text-success': recipe.difficulty === 'könnyű',
              'text-warning': recipe.difficulty === 'közepes',
              'text-danger': recipe.difficulty === 'nehéz',
            }">
              Nehézségi szint: {{ recipe.difficulty }}
            </p>
            <button class="btn btn-primary">Részletek</button>
          </div>
        </div>
      </div>
    </div>
  </div>

  <div v-if="activeTab === 'ujReceptek'" class="container my-4">
    <h3>Új recept hozzáadása</h3>
    <form @submit.prevent="addNewRecipe">
      <div class="mb-3">
        <label for="recipeName" class="form-label">Recept neve</label>
        <input type="text" id="recipeName" class="form-control" v-model="newRecipeName" required />
      </div>

      <div class="mb-3">
        <label for="cookTime" class="form-label">Elkészítési idő (perc)</label>
        <input type="number" id="cookTime" class="form-control" v-model="newRecipeCookTime" required />
      </div>

      <div class="mb-3">
        <label for="difficulty" class="form-label">Nehézségi szint</label>
        <select id="difficulty" class="form-select" v-model="newRecipeDifficulty" required>
          <option value="">Válassz nehézségi szintet</option>
          <option value="könnyű">Könnyű</option>
          <option value="közepes">Közepes</option>
          <option value="nehéz">Nehéz</option>
        </select>
      </div>

      <button type="submit" class="btn btn-success">Hozzáadás</button>
    </form>
  </div>
</template>

<style scoped>
.navbar-brand {
  font-weight: bold;
}

.nav-item .nav-link {
  text-transform: capitalize;
}

.text-success {
  font-weight: bold;
}

.text-warning {
  font-weight: bold;
}

.text-danger {
  font-weight: bold;
}
</style>
