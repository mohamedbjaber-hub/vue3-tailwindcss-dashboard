<template>
    <div class="bg-base-100 p-6 rounded-xl shadow-md  dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter(10px)] dark:border-white/20 mb-6">
        <h2 class="text-lg font-semibold">distribution des produit par region</h2>
        <Bar :data="stackedBarData" :options="stackedBarOptions" class="max-h-[400px]" />

        
    </div>
</template>
<script setup>
import { ref } from 'vue';
import { Bar } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale);

const stackedBarData = {
    labels: ['Q1', 'Q2', 'Q3', 'Q4'],
    datasets: [
        {
            label: 'Nord',
            backgroundColor: '#4635B1',
            data: [3200, 2900, 4200, 5100],
            stack: 'Region'
        },
        {
            label: 'Sud',
            backgroundColor: '#E82561',
            data: [3000, 5000, 2950, 4000],
            stack: 'Region'
        },
        {
            label: 'Ouest',
            backgroundColor: '#FFA24C',
            data: [2000, 3000, 5000, 4000],
            stack: 'Region'
        },
        {
            label: 'Est',
            backgroundColor: '#00C9A7',
            data: [5500, 1900, 2100, 2500],
            stack: 'Region'
        }
    ]
};

const stackedBarOptions = {
    responsive: true,
    maintainAspectRatio: false,
    plugins: {
        legend: {
            position: 'top',
            labels: {
                color: '#64748B', // Couleur des labels de la légende
                boxWidth: 12,
                padding: 16,
                usePointStyle: true,
            }
        },
        title: {
            display: false,
        },
        tooltip: {
            afterLabel: function(context) {
                let total = 0;
                const data = context.dataset.data;
                data.forEach(value => {
                    total += value;
                });
                const percentage = ((context.parsed.y / total) * 100).toFixed(2);
                return 'Percentage: ' + percentage + '%';
            }
        }
    },
    scales: {
        x: {
            stacked: true,
            grid: {
               display: false
            },
            ticks: {
                color: 'rgb(0,0,0,0.1)' // Couleur des ticks
            }
        },
        y: {
            stacked: true,
            grid: {
                color: 'rgb(0,0,0,0.5)',
            },
            ticks: {
                color: '#64748B', // Couleur des ticks
                callback: function(value) {
                    return value.toLocaleString() + ' $'; // Ajouter le symbole de dollar aux ticks
            }
        }
    }
}
};

</script>