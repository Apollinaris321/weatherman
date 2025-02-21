<template>
  <div class="container">
    <Snowflake ref="snowflake1" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake2" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake3" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake4" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake5" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake6" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake7" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake8" class="snowflake"></Snowflake>

    <Snowflake ref="snowflake9" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake10" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake11" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake12" class="snowflake"></Snowflake>
    <Snowflake ref="snowflake13" class="snowflake"></Snowflake>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import Snowflake from '@/components/icons/Snowflake.vue'
import gsap from 'gsap'

const snowflake1 = ref(null)
const snowflake2 = ref(null)
const snowflake3 = ref(null)
const snowflake4 = ref(null)
const snowflake5 = ref(null)
const snowflake6 = ref(null)
const snowflake7 = ref(null)
const snowflake8 = ref(null)
const snowflake9 = ref(null)
const snowflake10 = ref(null)
const snowflake11 = ref(null)
const snowflake12 = ref(null)
const snowflake13 = ref(null)

const clouds = ref(null)

const singlesnow1 = ref(null)

onMounted(() => {
  /*
  gsap.to(singlesnow1.value.$el, {
    scale: 1.1,
    duration: 3,
    ease: 'linear',
    yoyo: true,
    repeat: -1,
  })
  gsap.to(singlesnow1.value.$el, {
    duration: 30,
    rotation: 360,
    ease: 'linear',
    repeat: -1,
  })

  gsap.to(clouds.value.$el, {
    scale: 1.1,
    duration: 4,
    ease: 'linear',
    yoyo: true,
    repeat: -1,
  })

  gsap.set(snowflake1.value.$el, { x: 20 })
  gsap.set(snowflake1.value.$el, { y: 20 })
  gsap.to(snowflake1.value.$el, {
    y: 200,
    x: 50,
    duration: 1,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake2.value.$el, { x: 35 })
  gsap.set(snowflake2.value.$el, { y: 20 })
  gsap.to(snowflake2.value.$el, {
    y: 200,
    x: 60,
    duration: 0.8,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake3.value.$el, { x: 55 })
  gsap.set(snowflake3.value.$el, { y: 20 })
  gsap.to(snowflake3.value.$el, {
    y: 200,
    x: 90,
    duration: 0.8,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake4.value.$el, { x: 70 })
  gsap.set(snowflake4.value.$el, { y: 20 })
  gsap.to(snowflake4.value.$el, {
    y: 300,
    x: 100,
    duration: 1.2,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake5.value.$el, { x: 90 })
  gsap.set(snowflake5.value.$el, { y: 20 })
  gsap.to(snowflake5.value.$el, {
    y: 200,
    x: 120,
    duration: 1.4,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake6.value.$el, { x: 90 })
  gsap.set(snowflake6.value.$el, { y: 20 })
  gsap.to(snowflake6.value.$el, {
    y: 200,
    x: 120,
    duration: 1.4,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake7.value.$el, { x: 100 })
  gsap.set(snowflake7.value.$el, { y: 10 })
  gsap.to(snowflake7.value.$el, {
    y: 200,
    x: 100,
    duration: 2,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake8.value.$el, { x: 100 })
  gsap.set(snowflake8.value.$el, { y: 10 })
  gsap.to(snowflake8.value.$el, {
    y: 200,
    x: 150,
    duration: 1,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake9.value.$el, { x: 10 })
  gsap.set(snowflake9.value.$el, { y: 25 })
  gsap.to(snowflake9.value.$el, {
    y: 200,
    x: 20,
    duration: 3,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake10.value.$el, { x: 30 })
  gsap.set(snowflake10.value.$el, { y: 25 })
  gsap.to(snowflake10.value.$el, {
    y: 200,
    x: 20,
    duration: 3,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })

  gsap.set(snowflake10.value.$el, { x: 70 })
  gsap.set(snowflake10.value.$el, { y: 25 })
  gsap.to(snowflake10.value.$el, {
    y: 200,
    x: 20,
    duration: 3,
    ease: 'linear',
    repeat: -1,
    opacity: 1,
  })
  */
  gsap.set(snowflake1.value.$el, { x: 70 })
  gsap.to(snowflake1.value.$el, {
    y: 80,
    duration: 3,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.set(snowflake2.value.$el, { x: 10 })
  gsap.to(snowflake2.value.$el, {
    y: 80,
    duration: 5,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.set(snowflake3.value.$el, { x: 5 })
  gsap.to(snowflake3.value.$el, {
    y: 80,
    duration: 2.5,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.set(snowflake4.value.$el, { x: 30 })
  gsap.to(snowflake4.value.$el, {
    y: 90,
    duration: 2.8,
    rotate: 180,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.set(snowflake5.value.$el, { x: 90 })
  gsap.to(snowflake5.value.$el, {
    y: 90,
    duration: 2.2,
    ease: 'linear',
    opacity: 1,
    repeat: -1,
  })
  gsap.set(snowflake6.value.$el, { x: 80 })
  gsap.to(snowflake6.value.$el, {
    y: 90,
    duration: 3,
    ease: 'linear',
    opacity: 1,
    repeat: -1,
  })
  gsap.set(snowflake7.value.$el, { x: 60 })
  gsap.to(snowflake7.value.$el, {
    y: 90,
    duration: 3.5,
    rotate: 180,
    ease: 'linear',
    opacity: 0.8,
    repeat: -1,
  })

  gsap.set(snowflake8.value.$el, { x: 95 })
  gsap.to(snowflake8.value.$el, {
    y: 90,
    duration: 3.8,
    ease: 'linear',
    opacity: 0.8,
    repeat: -1,
  })

  gsap.set(snowflake9.value.$el, { x: 25 })
  gsap.to(snowflake9.value.$el, {
    y: 90,
    duration: 3.2,
    ease: 'linear',
    opacity: 0.8,
    repeat: -1,
  })
  gsap.set(snowflake10.value.$el, { x: 25 })
  gsap.to(snowflake10.value.$el, {
    y: 90,
    duration: 2.2,
    ease: 'linear',
    opacity: 0.4,
    repeat: -1,
  })
  gsap.set(snowflake11.value.$el, { x: 10 })
  gsap.to(snowflake11.value.$el, {
    y: 50,
    duration: 3,
    rotate: 180,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.set(snowflake12.value.$el, { x: 35 })
  gsap.to(snowflake12.value.$el, {
    y: 90,
    duration: 3,
    rotate: 180,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
  gsap.set(snowflake13.value.$el, { x: 28 })
  gsap.to(snowflake13.value.$el, {
    y: 60,
    duration: 4,
    rotate: 180,
    ease: 'linear',
    opacity: 0,
    repeat: -1,
  })
})
</script>

<style scoped>
.container2 {
  width: 150px;
  height: 200px;
  background-color: lightgray;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

.singlesnow {
  height: 50%;
  width: 50%;
}

.clouds {
  position: absolute;
  height: 100%;
  width: 100%;
}

@keyframes cloudmove {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.03);
  }
  100% {
    transform: scale(1);
  }
}

.snowflake {
  position: absolute;
  height: 10%;
  width: 10%;
}

.container {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}
</style>
