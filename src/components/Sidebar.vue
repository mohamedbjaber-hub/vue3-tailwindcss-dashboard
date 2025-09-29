<template>
  <aside
    class="drawer-side bg-white dark:bg-backgroundDark border-r border-gray-200 dark:border-primary/10"
  >
    <label
      for="my-drawer"
      class="drawer-overlay"
      aria-label="close sidebar"
    ></label>
    <nav
      class="menu p-4 w-80 text-gray-800 dark:text-gray-200"
      aria-label="Main navigation"
    >
      <header class="mb-4 flex p-4">
        <h1 class="text-xl font-bold dark:text-white">Admin Panel</h1>
      </header>
      <ul role="menu">
        <li role="none" class="p-2" v-for="(link, index) in links" :key="index">
          <button role="menuitem" 
          :aria-expanded="!!link.children && link.open"
          :aria-haspopup="!!link.children"
          :class="{'active':link.active}"
          @click="setActive(index)"
          class="flex items-center w-full text-left hover:bg-gray-100 text-black dark:hover:bg-white/10 dark:text-white">

            <Icon :icon="link.icon" class="w-5 h-5" />
            <span class="ml-2">{{ link.name }}</span>
            <span v-if="link.children">
                <Icon v-if="link.open" icon="line-md:chevron-up" class="w-4 h-4 ml-auto" />
                <Icon v-else icon="line-md:chevron-down" class="w-4 h-4 ml-auto" />
            </span>
        </button>
        <ul v-if="link.children && link.open"
        class="ml-4 pl-4 border-l border-gray-200 dark:border-white/10">
          <li v-for="(child, childIndex) in link.children" :key="childIndex">
            <a href="#" 
            class="block py-2 hover:bg-gray-100 dark:hover:bg-white/10 text-black dark:text-white ">
              {{ child.name }}
            </a>
            
          </li>
        </ul>
        </li>
      </ul>
    </nav>
  </aside>
</template>
<script setup>
import { ref } from "vue";
const links = ref([
  { 
    name: "Dashboard",
    icon: "line-md:home",
    active: true,
    open: false
  },
  {
    name: "Reports",
    icon: "line-md:document-list",
    active: false,
    open: false,
  },
  {
    name: "Utilisateurs",
    icon: "line-md:account",
    active: false,
    open: true,
    children: [
      { name: "Tous les utilisateurs" },
      { name: "Ajouter un utilisateur" },
      { name: "Rôles des utilisateurs" },
    ],
  },
  {
    name: "Produits",
    icon: "mdi:shopping-outline",
    active: false,
    open: false,
    children: [
      { name: "Tous les produits" },
      { name: "Catégories" },
      { name: "Inventaire" },
    ],
  },
  {
    name: "Messages",
    icon: "line-md:email",
    active: false,
    open: false,
  },
  {
    name: "Paramètres",
    icon: "line-md:cog",
    active: false,
    open: false,
  },
]);
const setActive = (index) => {
    // toggle open state for items with children
    if(links.value[index].children){
        links.value[index].open = !links.value[index].open;
    } 
    // set active state
    links.value.forEach((link, i) => {
        link.active = i === index;
    });

};
</script>
