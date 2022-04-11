<script setup>
import { computed, onMounted, ref } from 'vue'
import { useSectionsStore } from '~/stores/sections'
// States for the component
const active = ref(false)

const subSections = ref([])
onMounted(() => {
  const h2Array = document.querySelectorAll('h2')
  h2Array.forEach((h2) => {
    subSections.value.push(h2.innerText)
  })
})

</script>

<template>
  <div absolute right-3 top-4 w-58 class="miniNavigationBar">
    <span font-medium uppercase text-xs text-blue-200>На этой странице</span>
    <ul text-xs>
      <li v-for="subsection in subSections" :key="subsection" mt-2>
        <a :href="`#${subsection}`" text-gray-700 dark:text-gray-200 cursor-pointer hover:opacity-100 :class="[active? 'opacity-100' : 'opacity-80']">{{ subsection }}</a>
      </li>
    </ul>
  </div>
</template>

<style lang="scss" scoped>
.miniNavigationBar{
  visibility: hidden;
  @media (min-width: 1650px) {
    visibility: visible;
   }
}
</style>
