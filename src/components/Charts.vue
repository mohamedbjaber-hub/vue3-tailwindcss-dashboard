<template >
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
        <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20">
            <h2 class="text-lg font-semibold mb-4">Monthly Revenue</h2>
            <Line :data="revenuChartData" :options="lineChartOptions" class="max-h-[300px]" :key="lineChartKey" />
        </div>
        <!-- Doughnut Chart -->
        <div class="bg-base-100 p-6 rounded-xl shadow-md dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter:blur(10px)] dark:border-white/20">
            <h2 class="text-lg font-semibold mb-4">Source de revenue</h2>
            <Doughnut :data="doughnutChartData" :options="doughnutChartOptions" class="max-h-[300px]" :key="doughnutChartKey" />
        </div>
    </div>
</template>
<script setup>
import { Line, Doughnut } from 'vue-chartjs'
import { ref, onMounted } from 'vue';
import {
    Chart as ChartJS,
    Title,
    Tooltip,
    Legend,
    LineElement,
    CategoryScale,
    LinearScale,
    PointElement,
    ArcElement
} from 'chart.js';

ChartJS.register(
    Title,
    Tooltip,
    Legend,
    LineElement,
    CategoryScale,
    LinearScale,
    PointElement,
    ArcElement
);
const lineChartKey = ref(0);
const revenuChartData = ref({
    labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun',],
    datasets: [
        {
            label: 'Revenue ($)',
            backgroundColor: 'rgba(54, 162, 235, 0.2)',
            borderColor: 'rgba(54, 162, 235, 1)',
            data: [3000, 4000, 7000, 6000, 5000, 8000],
            fill: true,
            borderColor:"#E82561",
            tension: 0.4,
            backgroundColor: "#E82561",
        },
    ],
});
const lineChartOptions =ref( {
    responsive: true,
    maintainAspectRatio: false,
    animations: {
        tension: {
            duration: 1000,
            easing: 'linear',
            from: 1,
            to: 0,
            loop: false
        }
    },
    scales: {
        x: {
            grid: {
                color: 'rgba(0, 0, 0, 0.1)', // Couleur des lignes de la grille en mode sombre
            },
            ticks: {
                color: '#64748b', // Couleur des ticks en mode sombre
            },
        },
        y: {
            grid: {
                color: 'rgba(0, 0, 0, 0.1)', // Couleur des lignes de la grille en mode sombre
            },
            ticks: {
                color: '#64748b', // Couleur des ticks en mode sombre
            },
        },
    },
    plugins: {
        legend: {
            labels: {
                color: '#64748b', // Couleur des labels en mode sombre
            },
        },
        title: {
            display: false,
            text: 'Monthly Revenue',
        },
    },
}); 

const doughnutChartKey = ref(0);
const doughnutChartData = ref({
    labels: ['Products', 'Services', 'Subscriptions', 'Consulting'],
    datasets: [
        {
            label: 'Traffic Source',
            data: [35, 25, 20, 20],
            backgroundColor: [
                '#4635B1',
                '#E82561',
                '#ECE852',
                '#FFA24C'
            ],
            borderWidth: 0,
            hoverOffset: 10,
        }
    ]
});

const doughnutChartOptions = ref({
    responsive: true,
    maintainAspectRatio: false,
    cutout: '70%',
    animations: {
        duration: 1000,
        easing: 'easeOutQuart',
        animateScale: true,
        animateRotate: true,
    },
    plugins: {
        legend: {
            position: 'right',
            labels: {
                color: '#64748b',
                boxesWidth: 12,
                padding: 16,
            },
        },
        tooltip: {
            callbacks: {
                label: function (tooltipItem) {
                    return tooltipItem.label + ': ' + tooltipItem.raw + '%';
                }
            }
        }
    },
});
onMounted(() => {
    // Pour forcer le rechargement du graphique en mode sombre
    lineChartKey.value += 1;
    doughnutChartKey.value += 1;
});

</script>