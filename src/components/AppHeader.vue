<template>
    <header>
        <input type="text" placeholder="Suche...">
    </header>
</template>

<script>

    export default { 
        name: 'AppHeader',
    }

</script>

<style scoped>
header {
    background-color: #F4BC39;
    height: 120px;
    padding: 16px;
    display: flex;
    align-items: flex-end;
}

input {
    border: 0;
    border-radius: 8px;
    width: 100%;
    height: 30px;
}
</style>