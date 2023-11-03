<script setup>
import { computed } from '@vue/reactivity';
import { onMounted, ref, watch } from 'vue';
import SearchList from './SearchList.vue';
import SearchToolBar from './SearchToolBar.vue';
import SearchItem from './SearchItem.vue'

let items = ref([])
let searchQuery = ref('');
let relevantItems = ref([])

watch(searchQuery, async () => {
    if (searchQuery.value) {
        relevantItems.value = items.value.filter(item => (item.fullName || '').toLocaleLowerCase().includes(searchQuery.value.toLocaleLowerCase()))
        return;
    }
    relevantItems.value = items.value;
})

watch(items, async () => {
    relevantItems.value = items.value;
})

onMounted(() => {
    getItems();
})

const updateSearchQuery = (searchTerm) => searchQuery.value = searchTerm;

async function getItems() {
    return new Promise((resolve) => {
        setTimeout(async () => {
            const people = await fetch('/mock-data/people.json')
            items.value = formatData((await people.json()));
            return Promise.resolve();
        }, 0)
    })
}

function formatData(data) {
    return data.map(item => {
        item.key = Math.random() * data.length
        item.DOB = new Date(item.DOB).toDateString();
        return item;
    })
}

</script>

<template>
    <div class="search-container">
        <SearchToolBar @search-change="updateSearchQuery" />
        <SearchList v-if="items.length > 0" :items="relevantItems" />
        <v-progress-circular v-else indeterminate></v-progress-circular>
    </div>
</template>

<style scoped>
.search-container {
    width: 450px;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.v-progress-circular {
    width: 25px;
}
</style>