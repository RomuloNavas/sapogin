<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'
const mainContent = ref(null)
onMounted(() => {
  const h2Array = mainContent.value.querySelectorAll('h2')
  // ! Don't include in the subtitles the symbol: ?
  h2Array.forEach((h2) => {
    h2.setAttribute('id', h2.innerText)
  })
  const aArray = mainContent.value.querySelectorAll('a')
  aArray.forEach((a, index) => {
    // eslint-disable-next-line no-console
    console.log(a)
    a.classList.add('btn')
    a.setAttribute('href', `${h2Array[index].innerText}.pdf`)
  })
})
function goToTop() {
  const title = document.querySelector('h1')
  title.scrollIntoView({ behavior: 'smooth', block: 'start', inline: 'nearest' })
}
</script>

<template>
  <div class="flex flex-row h-screen bg-slate-100 dark:bg-slate-800 text-gray-800">
    <SideBar />
    <MiniNavigationBar />
    <main class="main flex flex-col flex-grow -ml-64 md:ml-0 transition-all duration-150 ease-in text-gray-700 dark:text-gray-200 overflow-y-auto">
      <div ref="mainContent" class="main-content flex flex-col flex-grow p-4 h-full text-center ">
        <router-view />
      </div>
      <button type="button" class="btn absolute right-3 bottom-4" @click="goToTop">
        <div i-carbon-arrow-up inline-block />
      </button>
    </main>
  </div>
</template>
