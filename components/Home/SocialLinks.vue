<template>
   <div>
      <div class="h-1.5 w-1.5 rounded-full bg-current"></div>
      <h2 class="uppercase text-xs font-semibold text-primary-600 dark:text-primary-400 mb-4">FIND ME ON</h2>
      <div class="space-y-5">
         <NuxtLink v-for="link in links" :key="link.icon" :to="link.url" target="_blank" external class="flex items-end gap-4 text-primary-600 dark:text-primary-400 group">
            <span class="text-sm text-primary-600 dark:text-primary-400">
               {{ link.name }}
            </span>
            <div class="flex-1 border-b border-dashed border-gray-300 dark:border-gray-800 group-hover:border-gray-700"></div>
            <Icon :name="link.icon" class="w-6 h-6 text-primary-600 dark:text-primary-400"></Icon>
         </NuxtLink>
      </div>
   </div>
</template>

<script lang="ts" setup>
   const links = [
      {
         name: "Discord",
         url: "https://discord.com/users/626413361185292321",
         icon: "mdi:discord",
  },
      {
         name: "GitHub",
         url: "https://github.com/Drnk-28",
         icon: "mdi:github",
  },
      {
         name: "Tiktok",
         url: "https://www.tiktok.com/@drnk.28",
         icon: "mdi:music-note",
  },
      {
         name: "Instagram",
         url: "https://instagram.com/drnk.28",
         icon: "mdi:instagram",
  },
];
</script>