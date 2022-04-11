<script setup lang="ts">
import { toggleDark } from '~/composables'
</script>

<template>
  <button class="btn" title="Toggle Dark mode" @click="toggleDark()">
    <div i="carbon-moon dark:carbon-sun" />
  </button>
</template>
