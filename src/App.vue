<template>
    <AppHeader></AppHeader>
    <RecipeItem></RecipeItem>
</template>

<script>
import AppHeader from './components/AppHeader.vue';
import RecipeItem from './components/RecipeItem.vue';

export default {
  name: 'App',
  components: {
    AppHeader,
    RecipeItem
  }
}
</script>

<style>
#app {
  font-family: Gill Sans, 'Gill Sans MT', 'Calibri', 'Trebuchet MS', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
}

body {
  margin: 0;
}
</style>
