<script setup>
import { reactive, toRefs } from 'vue'
import SearchItem from './SearchItem.vue'

defineProps(['items'])

</script>

<template>
    <div class="search-list-container">
        <SearchItem v-for="item in items" :item="item" />
    </div>
</template>

<style scoped>
.search-list-container {
    display: flex;
    flex-direction: column;
    gap: 8px;
}
</style>