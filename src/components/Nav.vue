<template lang="pug">
  nav
    RouterLink(to="/") Home
    RouterLink(to="/about") About
  RouterView
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>
