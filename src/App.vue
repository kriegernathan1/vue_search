<script setup>
import Search from './components/search/Search.vue'

</script>

<template>
    <div class="app-container">
        <h1>People Search</h1>
        <Search />
    </div>
</template>

<style scoped>
.app-container {
    width: 100vw;
    display: flex;
    gap: 10px;
    flex-direction: column;
    align-items: center;
    padding: 1rem;
    height: 100vh;
    overflow: hidden;
}
</style>
