<template lang="pug">
  Logo
  figure(v-for="projectdetail in projectdetails",)
    RouterLink(:to="{name: 'project', params: {id:projectdetail.id}}")
      img.homeImg(
        :key="projectdetail.id",
        :src="projectdetail.images[0]",
        :alt="projectdetail.title")
</template>

<script setup>
import Logo from "@/components/Logo.vue";
import projectData from "@/projectData.js";
import {RouterLink} from "vue-router";


const projectdetails = projectData.projectdetails

</script>

<style scoped>
.homeImg {
  width: 50vw;
  margin: 20vh 0 10vh 0;
}
@media screen and (max-width: 1025px) {
  .homeImg {
    margin: 10vh 0 10vh 10vw;
    width: 75vw;
  }
}
</style>
