<script setup>
import { computed } from '@vue/reactivity';
import { ref } from 'vue'

const { item } = defineProps(['item'])

const colorMap = new Map();
colorMap.set('Applied', 'green')
colorMap.set('In Progress', '#28456c')
colorMap.set('Rejected', '#cf4040')

const color = computed(() => {
    return colorMap.get(item.status) ?? '#363333';
})
</script>

<template>
    <div v-if="item" :key="item.key">
        <v-card width="400" :title="item.fullName" :subtitle="item.DOB">
            <v-card-text>
                <div class="status" :style="{ color }">{{ item.status }} </div>
            </v-card-text>
        </v-card>
    </div>
</template>


<style scoped>
.status {
    font-weight: bolder;
}
</style>