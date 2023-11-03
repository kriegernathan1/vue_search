<script setup>
import { toRefs } from 'vue'
defineProps(['item'])
</script>

<template>
    <div v-if="item">
        <v-card width="400" :title="item.fullName" :subtitle="item.DOB" :text="item.status"></v-card>
    </div>
</template>


<style scoped></style>