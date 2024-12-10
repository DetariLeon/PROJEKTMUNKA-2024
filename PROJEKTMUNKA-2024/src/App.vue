<script setup>
import RecipeCard from './components/RecipeCard.vue';
import { recipes } from './assets/dummyData';
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
        <input type="text" class="form-control" placeholder="Keresés recept név alapján..." />
      </div>

      <div class="col-md-3">
        <select class="form-select">
          <option selected>Nehézségi szint</option>
          <option value="könnyű">Könnyű</option>
          <option value="közepes">Közepes</option>
          <option value="nehéz">Nehéz</option>
        </select>
      </div>

      <div class="col-md-3">
        <select class="form-select">
          <option selected>Elkészítési idő</option>
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
      <div class="col-md-4" v-for="recipe in recipes" :key="recipe.id">
        <div class="card h-100">
          <img :src="recipe.imageUrl" class="card-img-top" alt="recipe.name" style="height: 200px; object-fit: cover;" />
          <div class="card-body">
            <h5 class="card-title">{{ recipe.name }}</h5>
            <p class="card-text">
              Elkészítési idő: {{ recipe.cookTime }} perc
            </p>
            <p
              class="card-text"
              :class="{
                'text-success': recipe.difficulty === 'könnyű',
                'text-warning': recipe.difficulty === 'közepes',
                'text-danger': recipe.difficulty === 'nehéz',
              }"
            >
              Nehézségi szint: {{ recipe.difficulty }}
            </p>
            <button class="btn btn-primary">Részletek</button>
          </div>
        </div>
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
