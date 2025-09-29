<template>
    <div class="card bg-base-100 dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter(10)] shadow-sm">
        <div class="card-body p-4">
            <h2 class="card-title text-lg font-semibold">Commandes récentes</h2>
            <div class="overflow-x-auto">
                <table class="table w-full">
                    <thead>
                        <tr>
                            <th>ID de commande</th>
                            <th>Consommateur</th>
                            <th>Date</th>
                            <th>Montant</th>
                            <th>Statut</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(order, index) in recentOrders" :key="index">
                            <td>{{ order.id }}</td>
                            <td>{{ order.customer }}</td>
                            <td>{{ order.date }}</td>
                            <td>{{ order.amount }}</td>
                            <td><span :class="`badge badge-${getStatusClass(order.status)}`">{{ order.status }}</span></td>
                        </tr>
                    </tbody>
                </table>
            </div>
            <div class="card-actions justify-end mt-4">
                <button class="btn btn-primary">Voir toutes les commandes</button>
            </div>
        </div>

    </div>
</template>
<script setup>
import { ref } from 'vue';

const recentOrders = ref([
    { id: "#12345", customer: 'John Doe', date: '01-01-2023', amount: 100, status: 'Pending' },
    { id: "#12346", customer: 'Jane Smith', date: '28-02-2024', amount: 200, status: 'Completed' },
    { id: "#12347", customer: 'Sam Johnson', date: '01-03-2025', amount: 150, status: 'Shipped' },
    { id: "#12348", customer: 'Alice Brown', date: '01-04-2025', amount: 250, status: 'Cancelled' },
]);
const getStatusClass = (status) => {
    const statusClasses = {
        Pending: 'warning',
        Completed: 'success',
        Shipped: 'info',
        Cancelled: 'error',
    };
    return statusClasses[status] || 'neutral';
};
</script>