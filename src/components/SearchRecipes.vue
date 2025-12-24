<template>
  <RecipeItem v-for="recipe in recipes" :key="recipe.idMeal" :label="recipe.strMeal" :category="recipe.strCategory"
    :image="recipe.strMealThumb" :recipe="recipe" @recipe-selected="storeSelectedRecipe" />

  <pre v-if="selectedRecipe">{{ selectedRecipe }}</pre>
</template>

<script>
import RecipeItem from './components/RecipeItem.vue'

export default {
  components: { RecipeItem },

  data() {
    return {
      recipes: [],          // 🔥 DAS ist gefüllt
      selectedRecipe: null
    }
  },

  methods: {
    storeSelectedRecipe(recipe) {
      this.selectedRecipe = recipe
      //console.log('Ausgewähltes Rezept:', recipe)
    }
  }
}
</script>

<style>

</style>