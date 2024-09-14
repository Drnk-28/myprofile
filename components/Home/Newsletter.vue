<template>
   <div>
      <div class="mb-6 flex items-center gap-3">
         <div class="flex-none rounded-full p-1 text-primary-500 bg-primary-500/10">
            <div class="h-1.5 w-1.5 rounded-full bg-current"></div>
         </div>
         <h2 class="uppercase text-xs font-semibold text-primary-600 dark:text-primary-400 mb-4">
            GIVE ME A MESSAGE
         </h2>

      </div>
      <p class="mt-2 text-sm text-gray-600 dark:text-gray-400">
         don't worry, we will never know who you are
      </p>
      <div class="flex items-center gap-3 mt-6">
         <UForm :validate="validate" :state="state" @submit="Write">
            <UFormGroup name="web">
               <UInput v-model="state.value" placeholder="write your message here" icon="solar-pen-linear" class="flex-1 w-6" size="lg" variant="outline" autocomplete="off" :ui="{ icon: { trailing: { pointer: '' } } }">
                  <template #trailing>
                     <UButton v-show="state.value !== ''" color="gray" icon="i-heroicons-x-mark-20-solid" @click="state.value = ''" />
                  </template>
               </UInput>
            </UFormGroup>
            <br>
            <UButton trailing block label="Send" icon="solar-plain-2-outline" size="lg" color="primary" type="submit" class="w-6"/>
         </UForm>
      </div>
   </div>
</template>

<script setup lang="ts">
   import { z } from "zod"
   import type { FormError, FormSubmitEvent } from '#ui/types'
   const toast = useToast()

   const state = reactive({
      value: undefined
   })

   const validate = (state: any): FormError[] => {
      const error = []
      if (state.value.length < 5) error.push({ path: "web", message: "Must be 5 or more characters" })
      if (state.value.length > 1200) error.push({ path: "web", message: "Must be less than 1200 characters" })

      return error
   }

   async function Write(event: FormSubmitEvent < any > ) {

      const urls = "https://discord.com/api/webhooks/1282822519853944903/dhZ1Ps9EByQ_KkE6Ql5mhbpwULmwQ6UFZTfy0GShasrvjp1-xiph1d0JOKaDVtF3_Z-T"
      const st = Date.now();
      let p = `<t:${parseInt(String(st).substr(0, String(st).length - 3))}:F>`

      await $fetch(urls, {
         method: "POST",
         headers: {
            "Content-Type": "application/json"
         },
         body: JSON.stringify({
            "embeds": [
               {
                  "color": 0x5865f2,
                  "fields": [
                     {
                        "name": `${p}`,
                        "value": `${event.data.value}`,
                        "inline": false
               }
               ]
            }
            ]
         })
      })
      state.value = ''
      toast.add({ title: "successfully", description: "your message has been sent" })
   }
</script>