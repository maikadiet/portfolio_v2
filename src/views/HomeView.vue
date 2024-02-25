<template lang="pug">
  Logo
  img(
    v-for="projectdetail in projectdetails",
    :src="`@/assets/${projectdetail.images[0]}`",
    :alt="projectdetail.title")
</template>

<script setup>
import Logo from "@/components/Logo.vue";
import projectData from "@/projectData.js";

const projectdetails = projectData.projectdetails

</script>

<style>
</style>
