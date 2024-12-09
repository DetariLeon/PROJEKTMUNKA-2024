<script setup>

</script>

<template>
  <nav class="navbar navbar-expand-lg bg-body-tertiary">
    <div class="container">
      <a class="navbar-brand" href="#">Receptkönyv</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
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
  <div class="container my-4">
    <div class="row g-4">
      <div class="col-md-4" v-for="recipe in recipes" :key="recipe.id">
        <RecipeCard
          :title="recipe.name"
          :description="'Elkészítési idő: ' + recipe.cookTime + ' perc'"
          :category="'Nehézségi szint: ' + recipe.difficulty"
          :imageSrc="recipe.imageUrl"
        />
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
