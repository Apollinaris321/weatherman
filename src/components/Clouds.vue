<template>
  <div class="containercloud">
    <!--
    <Cloud class="cloudanim1" />
    <Cloud class="cloudanim1 cloudanim2" />
    <Cloud class="cloudanim1 cloudanim3" />
    <Cloud class="cloudanim1 cloudanim4" />
    -->

    <Cloud class="cloud cloudanim1 cloudanim3"></Cloud>
    <Cloud class="cloud cloudanim1"></Cloud>

    <Cloud class="cloud cloudanim2"></Cloud>
    <Cloud class="cloud cloudanim2 cloudanim2-delay"></Cloud>
    <Cloud class="cloud cloudanim2 cloudanim3-delay"></Cloud>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Cloud from './icons/Cloud.vue'
</script>

<style scoped>
.cloud {
  position: absolute;
  top: 0;
  left: 0;
  height: 80%;
  width: 80%;
  display: block;
}

.containercloud {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.cloudanim1 {
  opacity: 0;
  animation: moving 20s linear infinite;
}

@keyframes moving {
  from {
    opacity: 1;
    transform: translateX(-200%) translateY(-30%);
  }
  to {
    opacity: 1;
    transform: translateX(300%) translateY(-30%);
  }
}

.cloudanim3 {
  animation-delay: -10s;
}
.cloudanim4 {
  animation-delay: -10s;
}

@keyframes moving-down {
  from {
    opacity: 1;
    transform: translateX(-120%);
  }
  to {
    opacity: 1;
    transform: translateX(200%);
  }
}

.cloudanim2 {
  opacity: 0;
  animation: moving-down 36s linear infinite;
}

.cloudanim2-delay {
  animation-delay: -12s;
}

.cloudanim3-delay {
  animation-delay: -24s;
}
</style>
