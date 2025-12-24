<template>
  <AppHeader v-model="query" />

  <p v-if="query && recipes.length === 0">
    Keine Rezepte gefunden
  </p>

  <!-- Scrollbarer Container für Rezepte -->
  <transition-group name="slide-fade" tag="div" class="recipes-container">
    <div
      v-for="recipe in filteredRecipes"
      :key="recipe.idMeal"
      class="recipe-wrapper"
    >
      <RecipeItem
        :label="recipe.strMeal"
        :category="recipe.strCategory"
        :image="recipe.strMealThumb"
        :recipe="recipe"
        @recipe-selected="handleRecipeClick"
      />
    </div>
  </transition-group>

  <!-- Detailansicht des ausgewählten Rezepts -->
  <div v-if="selectedRecipe" class="recipe-detail">
    <!-- Button zum Zurückgehen -->
    <button class="btn" @click="backToSearch">← Zurück zu den Suchergebnissen</button>

    <h2>{{ selectedRecipe.strMeal }}</h2>
    <p>{{ selectedRecipe.strInstructions }}</p>

    <!-- Button für aufklappbare Zutatenliste -->
    <button class="btn" @click="showIngredients = !showIngredients">
      {{ showIngredients ? 'Zutaten ausblenden' : 'Zutaten anzeigen' }}
    </button>

    <transition name="slide-fade-ingredients">
      <ul v-if="showIngredients">
        <li v-for="(item, index) in ingredientsList" :key="index">
          {{ item }}
        </li>
      </ul>
    </transition>
  </div>
</template>

<script>
import AppHeader from './components/AppHeader.vue'
import RecipeItem from './components/RecipeItem.vue'

export default {
  name: 'App',
  components: { AppHeader, RecipeItem },

  data() {
    return {
      query: '',
      recipes: [],
      selectedRecipe: null,
      showIngredients: false
    }
  },

  watch: {
    query() {
      this.fetchRecipes()
    }
  },

  computed: {
    filteredRecipes() {
      if (!this.selectedRecipe) return this.recipes
      return this.recipes.filter(
        recipe => recipe.idMeal === this.selectedRecipe.idMeal
      )
    },

    ingredientsList() {
      if (!this.selectedRecipe) return []
      const list = []
      for (let i = 1; i <= 20; i++) {
        const ingredient = this.selectedRecipe[`strIngredient${i}`]
        const measure = this.selectedRecipe[`strMeasure${i}`]
        if (ingredient && ingredient.trim() !== '') {
          list.push(`${ingredient} - ${measure}`)
        }
      }
      return list
    }
  },

  methods: {
    async fetchRecipes() {
      if (!this.query || this.query.length < 3) {
        this.recipes = []
        this.selectedRecipe = null
        this.showIngredients = false
        return
      }

      const url = `https://www.themealdb.com/api/json/v1/1/search.php?s=${this.query}`
      const resp = await fetch(url)
      const data = await resp.json()

      this.recipes = data.meals ?? []
    },

    handleRecipeClick(recipe) {
      this.selectedRecipe = recipe
      this.showIngredients = false
    },

    backToSearch() {
      this.selectedRecipe = null
      this.showIngredients = false
    }
  }
}
</script>

<style scoped>
/* Container für scrollbare Rezepte */
.recipes-container {
  max-height: calc(100vh - 80px);       /* Höhe nach Bedarf anpassen */
  overflow-y: auto;
  scrollbar-width: none;   /* Firefox */
}
.recipes-container::-webkit-scrollbar {
  display: none;           /* Chrome, Safari, Edge */
}

/* Wrapper für transition-group */
.recipe-wrapper {
  display: block;
  margin-bottom: 8px;
}

/* Slide & Fade Transition für Rezepte */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.5s ease;
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

.slide-fade-enter-to,
.slide-fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}

/* Slide & Fade für Zutatenliste */
.slide-fade-ingredients-enter-active,
.slide-fade-ingredients-leave-active {
  transition: all 0.3s ease;
}

.slide-fade-ingredients-enter-from,
.slide-fade-ingredients-leave-to {
  opacity: 0;
  max-height: 0;
}

.slide-fade-ingredients-enter-to,
.slide-fade-ingredients-leave-from {
  opacity: 1;
  max-height: 500px;
}

/* Recipe-Detail */
.recipe-detail {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid rgba(0,0,0,0.2);
  border-radius: 8px;
  background-color: #fafafa;
  transition: all 0.5s ease;
}

.recipe-detail button {
  margin: 10px 0;
  padding: 10px 12px;
  cursor: pointer;
}

/* Buttons */
.btn {
  border: none;
  border-radius: 50px;
  padding: 16px;
  background-color: #2c3e50;
  color: whitesmoke;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #4b5c70;
}

</style>

<style>
#app {
  font-family: Raleway;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
}

body {
  margin: 0;
  -ms-overflow-style: none;  /* IE & Edge */
  scrollbar-width: none;     /* Firefox */
}

body::-webkit-scrollbar {
  display: none; /* Chrome, Safari, Edge */
}

@font-face {
  font-family: "Raleway";
  src: url("@/assets/fonts/raleway-v34-latin-500.woff2") format("woff2");
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}
</style>
