<template>
  <h1 class="title">
    <Cloud class="cloud2"></Cloud>
    <div>W</div>
    <div>e</div>
    <div>a</div>
    <div>t</div>
    <div>h</div>
    <div>e</div>
    <div>r</div>
    <div>m</div>
    <div>a</div>
    <div>n</div>
    <Cloud class="cloud"></Cloud>
  </h1>
</template>

<script setup>
import Cloud from './icons/Cloud.vue'
</script>

<style scoped>
.title {
  font-size: 4em;
  margin: 0;
  padding: 0.5em;
  display: flex;
  flex-direction: row;
  overflow: hidden;
  width: 100%;
  align-items: center;
  justify-content: center;
  position: relative;
}

.title {
  animation: spread 1s ease-out forwards;
}

@keyframes spread {
  from {
    transform: translateX(-50%);
    opacity: 0;
  }
  to {
    transform: translateX(0%);
    opacity: 1;
  }
}

.title div {
  animation: tilt 1s ease-out forwards;
}

@keyframes tilt {
  0% {
    transform: rotate(20deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

.cloud {
  position: absolute;
  width: 40%;
  height: 40%;
  left: 36%;
  top: 47%;
  animation: scaling 5s linear infinite;
}

.cloud2 {
  position: absolute;
  width: 40%;
  height: 40%;
  left: 23%;
  top: 10%;
  z-index: -1;
  animation: scaling2 9s linear infinite;
}

@keyframes scaling {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.9) translateY(-1%);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes scaling2 {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.9) translateX(-1%);
  }
  100% {
    transform: scale(1);
  }
}
</style>
