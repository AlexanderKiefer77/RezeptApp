<template>
    <div class="recipeItemContainer">
        <img :src="image" alt="Rezeptbild" class="recipe-image" /> <!-- Bild als Variable eingebunden -->
        <div class="right-side">
            <div>
                {{ label }}
            </div>
            <div class="bottom-row">
                {{ attributes }}
            </div>
        </div>
    </div>
</template>

<script>
import logo from '@/assets/R1.png'  // Vue erkennt @ als src/ -- Bild wird Importiert

export default {
    name: 'RecipeItem',
    data() {
        return {
            image: logo,  // für Bild
            label: 'Ramen Menü 1',
            attributes: 'Vegan, Fettarm',
        }
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