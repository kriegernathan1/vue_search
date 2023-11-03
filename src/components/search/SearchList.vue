<script setup>
import { reactive, toRefs } from 'vue'
import SearchItem from './SearchItem.vue'

defineProps(['items'])

</script>

<template>
    <div class="search-list-container">
        <v-virtual-scroll :items="items">
            <template v-slot:default="{ item }">
                <SearchItem :item="item" />
            </template>
        </v-virtual-scroll>
    </div>
</template>

<style scoped>
.search-list-container :deep(.v-virtual-scroll__container) {
    display: flex;
    flex-direction: column;
    gap: 8px;
}
</style>