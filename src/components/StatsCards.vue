<template >
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 mb-6">
        <div v-for="(state,index) in stateData" :key="index" 
        class="stats bg-base-100 shadow dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)]
        dark:border-white/20">
        <div class="stat">
            <div class="stat-title">{{ state.title }}</div>
            <div class="stat-value">{{ state.value }}</div>
            <div class="stat-desc"
            :class="{'text-green-500':isPositifChange(state.description),
                'text-red-500':!isPositifChange(state.description)
            }">{{ state.description }}</div>
        </div>
    </div>
    </div>
</template>
<script setup>
import { ref } from 'vue';

const stateData = ref([
    { title: 'Total Users', value: '12,689', description:'↗ 9% from last month' },
    { title: 'Revenue', value: '$13,098', description: '↗ 31% from last month' },
    { title: 'New Order', value: '34', description: '↘ 26% from last month' },
    { title: 'Active Project', value: '56', description: '↘ 12% from last month' },
]);
const isPositifChange = (desc) => {
    return desc.includes('↗');
}
</script>