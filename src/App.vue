<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import Main from "./components/Main.vue";
import Footer from "./components/Footer.vue";

const containerHeight = ref(window.innerHeight);
const containerWidth = ref(window.innerWidth);

const updateDimensions = () => {
  containerHeight.value = window.innerHeight;
  containerWidth.value = window.innerWidth;
};

document.body.style.overflow = 'hidden';

onMounted(() => {
  window.addEventListener('resize', updateDimensions);
});

onUnmounted(() => {
  window.removeEventListener('resize', updateDimensions);
});
</script>

<template>
  <div class="container-fluid" :style="{ height: containerHeight + 'px', width: containerWidth + 'px' }">
    <Main />
    <Footer />
  </div>
</template>

<style scoped>
html, body {
    height: 100%;
    overflow: hidden;
}
.container-fluid {
    overflow: hidden;
}
.container, .container-fluid, .container-lg, .container-md, .container-sm, .container-xl, .container-xxl{
  padding-left: 0 !important;
  padding-right: 0 !important;
}
</style>
