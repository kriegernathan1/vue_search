<script setup>
import { watch, ref } from 'vue';

const emits = defineEmits(['search-change'])
const search = ref(null);

watch(search, () => {
    emits('search-change', search.value)
})
</script>

<template>
    <v-text-field v-model="search" label="Search"></v-text-field>
</template>

<style scoped>
.v-text-field {
    width: 100%;
}
</style>