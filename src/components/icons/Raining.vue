<template>
  <svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100" role="img">
    <line
      ref="line1"
      x1="10"
      y1="10"
      x2="10"
      y2="20"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line2"
      x1="35"
      y1="10"
      x2="35"
      y2="20"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />

    <line
      ref="line3"
      x1="70"
      y1="12"
      x2="70"
      y2="22"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line4"
      x1="95"
      y1="7"
      x2="95"
      y2="17"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />

    <line
      ref="line5"
      x1="22"
      y1="20"
      x2="22"
      y2="30"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line6"
      x1="49"
      y1="20"
      x2="49"
      y2="30"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />

    <line
      ref="line7"
      x1="79"
      y1="-20"
      x2="79"
      y2="-10"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line8"
      x1="65"
      y1="-20"
      x2="65"
      y2="-10"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line9"
      x1="5"
      y1="-20"
      x2="5"
      y2="-10"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />

    <line
      ref="line10"
      x1="61"
      y1="31"
      x2="61"
      y2="41"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line11"
      x1="5"
      y1="65"
      x2="5"
      y2="75"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line12"
      x1="40"
      y1="-20"
      x2="40"
      y2="-10"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />
    <line
      ref="line13"
      x1="15"
      y1="-10"
      x2="15"
      y2="-20"
      stroke="black"
      stroke-width="2"
      stroke-linecap="round"
    />

    <!--

    <line x1="45" y1="65" x2="45" y2="75" stroke="black" stroke-width="2" stroke-linecap="round" />
    <line x1="25" y1="69" x2="25" y2="79" stroke="black" stroke-width="2" stroke-linecap="round" />

    <line x1="95" y1="69" x2="95" y2="79" stroke="black" stroke-width="2" stroke-linecap="round" />
    <line x1="79" y1="73" x2="79" y2="83" stroke="black" stroke-width="2" stroke-linecap="round" />
    -->
  </svg>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'

const line1 = ref(null)
const line2 = ref(null)
const line3 = ref(null)
const line4 = ref(null)
const line5 = ref(null)
const line6 = ref(null)
const line7 = ref(null)
const line8 = ref(null)
const line9 = ref(null)
const line10 = ref(null)
const line11 = ref(null)
const line12 = ref(null)
const line13 = ref(null)

onMounted(() => {
  gsap.to(line1.value, {
    y: 80,
    duration: 1,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.to(line2.value, {
    y: 80,
    duration: 0.5,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.to(line3.value, {
    y: 80,
    duration: 1.5,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.to(line4.value, {
    y: 90,
    duration: 1.3,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.to(line5.value, {
    y: 90,
    duration: 2,
    ease: 'linear',
    opacity: 1,
    repeat: -1,
  })
  gsap.to(line6.value, {
    y: 90,
    duration: 1,
    ease: 'linear',
    opacity: 1,
    repeat: -1,
  })
  gsap.to(line7.value, {
    y: 90,
    duration: 1,
    ease: 'linear',
    opacity: 0.8,
    repeat: -1,
  })

  gsap.to(line8.value, {
    y: 90,
    duration: 1,
    ease: 'linear',
    opacity: 0.8,
    repeat: -1,
  })

  gsap.to(line9.value, {
    y: 90,
    duration: 1,
    ease: 'linear',
    opacity: 0.8,
    repeat: -1,
  })
  gsap.to(line10.value, {
    y: 90,
    duration: 2,
    ease: 'linear',
    opacity: 0.4,
    repeat: -1,
  })
  gsap.to(line11.value, {
    y: 50,
    duration: 1,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.to(line12.value, {
    y: 90,
    duration: 3,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.to(line13.value, {
    y: 60,
    duration: 3,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
})
</script>

<style scoped></style>
