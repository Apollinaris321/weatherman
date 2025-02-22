<script setup lang="ts">
import Moon from './Moon.vue'
import Star from './Star.vue'
</script>

<template>
  <div class="container-night">
    <Moon class="moon"></Moon>
    <Star class="star1"></Star>
    <Star class="star2"></Star>
  </div>
</template>

<style scoped>
.container-night {
  position: relative;
  width: 100%;
  height: 100%;
}

.moon {
  position: absolute;
  width: 70%;
  height: 70%;
  top: 20%;
  right: 25%;
  animation: moon 6s linear infinite;
}

@keyframes moon {
  50% {
    transform: rotate(8deg);
  }
}

.star1 {
  position: absolute;
  width: 20%;
  height: 20%;
  top: 40%;
  right: 15%;
  animation: star1 3s linear infinite;
}

@keyframes star1 {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1) rotate(-20deg);
  }
  100% {
    transform: scale(1);
  }
}

.star2 {
  position: absolute;
  width: 30%;
  height: 30%;
  top: 10%;
  right: 10%;
  animation: star2 3s linear infinite;
}

@keyframes star2 {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1) translateX(-3%);
  }
  100% {
    transform: scale(1);
  }
}
</style>
