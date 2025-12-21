<template>
  <AppHeader v-model="query" />

  <p v-if="query && recipes.length === 0">
    Keine Rezepte gefunden
  </p>

  <RecipeItem
    v-for="recipe in recipes"
    :key="recipe.idMeal"
    :label="recipe.strMeal"
    :category="recipe.strCategory"
    :image="recipe.strMealThumb"
  />
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
      recipes: []
    }
  },

  watch: {
    query() {
      this.fetchRecipes()
    }
  },

  methods: {
    async fetchRecipes() {
      if (!this.query || this.query.length < 2) {
        this.recipes = []
        return
      }

      const url = `https://www.themealdb.com/api/json/v1/1/search.php?s=${this.query}`
      const resp = await fetch(url)
      const data = await resp.json()

      this.recipes = data.meals ?? []
    }
  }
}


 /*async mounted() {
      /* Beispiel für die API Adresse mit Variablen. Diese API ist nicht mehr Kostenlos. 
         Diese wurde im Video verwendet. Ich habe auf die untere API gewechselt zum testen.
         const query = 'Sushi';
         const appId = 'd7212edc';
         const appKey = '3515d1c2238911f0dde38cb661b1f67e';
         const url = `https://api.edaman.com/search?q=${query}&app_id=${appId}&app_key=${appKey}`;
      */

    /*const query = 'curry'
    const url = `https://www.themealdb.com/api/json/v1/1/search.php?s=${query}`
    const resp = await fetch(url)
    const data = await resp.json()
    this.recipes = data.meals
    console.log(this.recipes);
  }*/
</script>


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
}

@font-face {
  font-family: "Raleway";
  src: url("@/assets/fonts/raleway-v34-latin-500.woff2") format("woff2");
  font-weight: 500;
  font-style: normal;
  font-display: swap;
}
</style>
