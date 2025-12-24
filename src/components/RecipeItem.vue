<template>
    <!-- <a :href="url" class="recipeItemContainer"> 
        Beispiel für einen Link zum original Rezept, ist bei der genutzten API nicht vorhanden.
    -->

  <div class="recipeItemContainer" @click="select">
    <img :src="image" class="recipe-image" />
    <div class="right-side">
      <div>{{ label }}</div>
      <div class="bottom-row">{{ category }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'RecipeItem',

  props: {
    label: String,
    category: String,
    image: String,
    recipe: Object
  },

  methods: {
    select() {
      this.$emit('recipe-selected', this.recipe)
    }
  }
}
</script>

<style scoped>

.recipeItemContainer {
  display: flex;
  gap: 8px;
  padding: 8px;
  border: 1px solid rgba(0,0,0,0.2);
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.3s ease;
}

.recipeItemContainer:hover {
  background-color: rgba(0,0,0,0.05);
}

.recipe-image {
  width: 60px;
}

.right-side {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.bottom-row {
  font-size: 12px;
  color: rgba(0,0,0,0.5);
}
</style>
