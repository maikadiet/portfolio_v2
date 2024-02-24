<template lang="pug">
  ul(id="nav")
    li
      RouterLink(to="/") work
    li ––
    li
      RouterLink(to="/about") about / contact
  RouterView
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<style scoped>
#nav {
  font-family: aktiv-grotesk-extended, sans-serif;
  bottom: 1.25vw;
  left: 2vw;
  transform-origin: left;
  transform: rotate(-90deg);
  position: fixed;
  color: black;
}
ul > li {
  list-style-type: none;
  margin-right: 10px;
  padding: 0;
  display: inline;
}
</style>
