<template>
  <svg
    ref="sun"
    xmlns="http://www.w3.org/2000/svg"
    width="100"
    height="100"
    viewBox="0 0 100 100"
    role="img"
  >
    <!-- Horizontal line at bottom -->
    <line
      ref="sunline1"
      x1="10"
      y1="50"
      x2="90"
      y2="50"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="sunline2"
      x1="50"
      y1="10"
      x2="50"
      y2="90"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />

    <line
      x1="10"
      y1="50"
      x2="90"
      y2="50"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
      transform="rotate(45,50,50)"
    />
    <line
      x1="50"
      y1="10"
      x2="50"
      y2="90"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
      transform="rotate(45,50,50)"
    />
    <circle cx="50" cy="50" r="25" fill="#fff" stroke-width="2" />
    <circle cx="50" cy="50" r="20" fill="#fff" stroke="#000000" stroke-width="2" />
  </svg>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'

const sun = ref(null)
const sunline1 = ref(null)
const sunline2 = ref(null)

onMounted(() => {
  gsap.to(sun.value, {
    rotation: 360,
    duration: 50,
    ease: 'linear',
    repeat: -1,
  })
  gsap.to(sunline1.value, {
    attr: {
      x1: '+=2', // Move left end right
      x2: '-=2', // Move right end left
    },
    duration: 1,
    ease: 'linear',
    yoyo: 1,
    repeat: -1,
  })
  gsap.to(sunline2.value, {
    attr: {
      y1: '+=2', // Move left end right
      y2: '-=2', // Move right end left
    },
    duration: 1,
    ease: 'linear',
    yoyo: 1,
    repeat: -1,
    delay: 0.5,
  })
})
</script>
<style scoped></style>
