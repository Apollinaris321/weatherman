<template>
  <div class="svg-main">
    <svg width="200" height="200" viewBox="0 0 200 200">
      <circle
        ref="circle"
        cx="100"
        cy="100"
        r="80"
        fill="none"
        stroke="#2196F3"
        stroke-width="10"
        stroke-linecap="round"
        :stroke-dasharray="dashArray"
        :stroke-dashoffset="dashOffset"
      />
    </svg>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'

const circle = ref(null)
const circumference = ref(0)
const dashLength = 10
const dashArray = ref('')
const dashOffset = ref(0)

onMounted(() => {
  const radius = 80
  circumference.value = 2 * Math.PI * radius

  // Create dash pattern: [visible segment] [invisible gap]
  dashArray.value = `${dashLength} ${circumference.value - dashLength}`

  // Animate the offset to make the segment move
  gsap.to(circle.value, {
    strokeDashoffset: circumference.value, // Full rotation
    duration: 3,
    ease: 'none',
    repeat: -1, // Infinite loop
  })
})
</script>
