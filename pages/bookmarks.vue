<template>
   <main class="min-h-screen">
      <AppHeader class="mb-8" title="Bookmarks" :description="description" />
      <ul class="space-y-2">
         <li v-for="bookmark in bookmarks" :key="bookmark.id">
            <a :href="bookmark.url" target="_blank" class="flex items-center gap-3 hover:bg-gray-100 dark:hover:bg-white/10 p-2 rounded-lg -m-2 text-sm min-w-0">
               <UAvatar :src="getThumbnail(bookmark.url)" :alt="bookmark.label" :ui="{ rounded: 'rounded-md' }" />
               <p class="truncate text-gray-700 dark:text-gray-200">
                  {{ bookmark.label }}
               </p>
               <span class="flex-1"></span>
               <span class="text-xs font-medium text-gray-400 dark:text-gray-600">
                  {{ getHost(bookmark.url) }}
               </span>
            </a>
         </li>
      </ul>
   </main>
</template>

<script setup>
   const description =
      "Awesome things I've found on the internet. This page is still WIP, I want to add search like bmrks.com";
   useSeoMeta({
      title: "Bookmarks | drnk.28",
      description,
   });

   const bookmarks = [
      {
         id: 1,
         label: "Adam Wathan - Tailwind CSS Best Practice Patterns",
         url: "https://www.youtube.com/watch?v=J_7_mnFSLDg",
      },
      {
         id: 2,
         label: "Beautiful Gradient Generator",
         url: "https://www.joshwcomeau.com/gradient-generator/",
  },
      {
         id: 3,
         label: "3D device mockups",
         url: "https://deviceframes.com/",
  },

];

   function getHost(url) {
      const parsedUrl = new URL(url);
      let host = parsedUrl.host;
      if (host.startsWith("www.")) {
         host = host.substring(4);
      }
      return host;
   }

   function getThumbnail(url) {
      const host = getHost(url);
      return `https://logo.clearbit.com/${host}`;
   }
</script>