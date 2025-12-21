<template>
    <!-- <a :href="url" class="recipeItemContainer"> 
        Beispiel für einen Link zum original Rezept, ist bei der genutzten API nicht vorhanden.
    -->
    <div class="recipeItemContainer">
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
        url: String,
    }
}
</script>


<style scoped>
.recipeItemContainer {
    border: 1px solid rgba(0, 0, 0, 0.2);
    padding: 8px;
    border-radius: 8px;
    margin: 8px;
    display: flex;
    gap: 8px;
    cursor: pointer;
}

.recipeItemContainer:hover {
    background-color: rgba(0, 0, 0, 0.1);
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
    color: rgba(0, 0, 0, 0.5);
    font-size: 12px;
}
</style>