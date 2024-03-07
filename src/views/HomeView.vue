<template lang="pug">
  Logo
  figure(v-for="projectdetail in projectdetails",)
    RouterLink(:to="{name: 'project', params: {id:projectdetail.id}}")
      img.homeImg(
        @mousemove="mouseMove",
        @mouseenter="mouseEnter(projectdetail.id)",
        @mouseleave="mouseLeave",
        :src="projectdetail.images[0]",
        :alt="projectdetail.title")
  h1.movingType(
    :id="'projectTitle'+projectdetail.id",
    v-show="visible && currentId === projectdetail.id",
    :style="{ top: titlePosition.y + 'px', left: titlePosition.x + 'px' }"
  ) {{ projectdetail.title}}
</template>

<script setup>
import Logo from "@/components/Logo.vue"
import projectData from "@/projectData.js"
import { RouterLink } from "vue-router"
import { ref, reactive, onMounted, onUnmounted } from "vue"
import { useMouse } from '@vueuse/core'
const { x, y } = useMouse({ touch: false })

const projectdetails = projectData.projectdetails
const visible = ref(true)
const currentId = ref(null)
const titlePosition = reactive({ x: 0, y: 0 })
let debounceTimer

function debounce(func, delay) {
  return function() {
    const context = this
    const args = arguments
    clearTimeout(debounceTimer)
    debounceTimer = setTimeout(() => func.apply(context, args), delay)
  }
}
function mouseEnter(id) {
  currentId.value = id
  visible.value = true
  titlePosition.x = x._rawValue
  titlePosition.y = y._rawValue
  window.addEventListener('mousemove', mouseMove, false)
}
function mouseLeave() {
  visible.value = false
  currentId.value = null
}
function mouseMove() {
  debounce(() => {
    if (currentId.value !== null) {
      titlePosition.x = x.value;
      titlePosition.y = y.value;
      console.log(titlePosition.x, titlePosition.y)
    }
  }, 5)(); // Adjust debounce delay as needed
}

onMounted(() => {
  window.addEventListener('mousemove', mouseMove);
});

onUnmounted(() => {
  window.removeEventListener('mousemove', mouseMove);
})


</script>

<style scoped>
.homeImg {
  width: 50vw;
  margin: 20vh 0 10vh 0;
}
.movingType {
  position: absolute;
  font-family: 'LeMurmure';
  font-size: 10vw;
  color: black;
}

@media screen and (max-width: 1025px) {
  .homeImg {
    margin: 10vh 0 10vh 10vw;
    width: 75vw;
  }
}
</style>
