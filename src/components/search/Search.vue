<script setup>
import SearchToolBar from './SearchToolBar.vue'
import SearchList from './SearchList.vue'
import { reactive, ref } from 'vue';
import { computed } from '@vue/reactivity';
import { def } from '@vue/shared';
import { onMounted } from 'vue';

let items = ref([])
let searchQuery = ref('');
const updateSearchQuery = (searchTerm) => searchQuery.value = searchTerm;

onMounted(() => {
    getItems();
})

let relevantItems = computed(() => {
    if (searchQuery.value) {
        return items.value.filter(item => (item.fullName || '').toLocaleLowerCase().includes(searchQuery.value.toLocaleLowerCase()))
    }
    return items.value;
})

async function getItems() {
    try {
        const people = await fetch('/mock-data/people.json')
        items.value = formatData((await people.json()).slice(0, 50));
    } catch {
        console.error("Something happened")
    }
}

function formatData(data) {
    return data.map(item => {
        item.DOB = new Date(item.DOB).toDateString();
        return item;
    })
}

</script>

<template>
    <div class="search-container">
        <SearchToolBar @search-change="updateSearchQuery" />
        <SearchList :items="relevantItems" />
    </div>
</template>

<style scoped>
.search-container {
    width: 450px;
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>