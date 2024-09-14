<script lang="ts" setup>
   const toast = useToast()
   const { locale, locales, setLocale } = useI18n()

   const aLang = computed(() => {
      let wht = locales.value.filter((y) => y.code !== locale.value)
      return wht
   })
</script>

<template>
   <UTooltip text="Language switcher" :ui="{ popper: { strategy: 'absolute' } }">
      <UButtonGroup v-for="item in aLang" :key="item.code" @click.prevent.stop="setLocale(item.code)" orientation="horizontal" class="relative px-3 py-4 flex items-center justify-center transition hover:text-primary-500 dark:hover:text-primary-400">
         <UButton :icon="{{item.icon}}" />
         <UButton :label="{{item.name}}" color="gray" />
      </UButtonGroup>
   </UTooltip>
</template>