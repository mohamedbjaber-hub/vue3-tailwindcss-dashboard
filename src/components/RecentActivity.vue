<template >
    <div class="card bg-base-100 dark:bg-white/5 dark:backdrop-blur-md dark:[--webkit-backdrop-filter(10px)] shadow-sm">
        <div class="card-body p-4">
            <h2 class="card-title">Activité récente</h2>
            <ul class="timeline timeline-vertical">
                <li v-for="(activity,index) in recentActivities" :key="index">
                   <template v-if="index % 2 === 0">
                       <div class="timeline-start timeline-box bg-white dark:bg-backgroundDark">
                              {{ activity.type }}
                       </div>
                       <div class="timeline-middle">
                        <Icon icon="line-md:circle-filled-to-confirm-circle-filled-transition" class="w-5 h-5 text-primary" />
                       </div>
                       <hr class="bg-primary" />
                   </template>
                   <template v-else>
                       <hr class="bg-primary" />
                       <div class="timeline-middle">
                           <Icon icon="line-md:circle-filled-to-confirm-circle-filled-transition" class="w-5 h-5 text-primary" />
                       </div>
                       <div class="timeline-end timeline-box bg-white dark:bg-backgroundDark">
                              {{ activity.type }}
                       </div>
                       <hr class="bg-primary" />
                   </template>
               </li>
            </ul>
            
        </div>
        
    </div>
</template>
<script setup>
import { Icon } from '@iconify/vue';
import { ref } from 'vue';
const recentActivities = ref([
    { type: 'Connection utilisateur', time:'09:45AM', icon:'check' },
    { type: 'Commande passée', time:'09:50AM', icon:'check' },
    { type: 'Produit ajouté', time:'09:55AM', icon:'check' },
    { type: 'Utilisateur mis à jour', time:'10:00AM', icon:'check' },
    { type: 'Rapport généré', time:'10:05AM', icon:'check' },
]);

</script>