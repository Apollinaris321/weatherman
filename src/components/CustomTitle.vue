<template>
  <h1 class="title">
    <Cloud class="cloud1"></Cloud>
    <div class="letter">
      <div class="letter0" id="letter">W</div>
    </div>
    <div class="letter">
      <div class="letter1">e</div>
    </div>
    <div class="letter">
      <div class="letter2">a</div>
    </div>
    <div class="letter">
      <div class="letter3">t</div>
    </div>
    <div class="letter">
      <div class="letter4">h</div>
    </div>
    <div class="letter">
      <div class="letter5">e</div>
    </div>
    <div class="letter">
      <div class="letter6">r</div>
    </div>
    <div class="letter">
      <div class="letter7">m</div>
    </div>
    <div class="letter">
      <div class="letter8">a</div>
    </div>
    <div class="letter">
      <div class="letter9">n</div>
    </div>
    <div class="letter">
      <div class="letter10">.</div>
    </div>
    <Cloud class="cloud2" id="cloud"></Cloud>
  </h1>
</template>

<script setup>
import Cloud from './icons/Cloud.vue'
import gsap from 'gsap'
import { onMounted, onUnmounted, ref } from 'vue'

onMounted(() => {
  gsap.fromTo(
    '.cloud1',
    {
      x: -500,
      y: -50,
    },
    {
      x: 500,
      y: -50,
      duration: 15,
      ease: 'linear',
      repeat: -1,
    },
  )

  gsap.fromTo(
    '.cloud2',
    {
      x: -500,
      y: 30,
    },
    {
      x: 500,
      y: 30,
      duration: 10,
      ease: 'linear',
      repeat: -1,
    },
  )
})
</script>

<style scoped>
.title {
  font-size: 4em;
  margin: 0;
  padding: 0.5em;
  display: flex;
  flex-direction: row;
  width: 100%;
  align-items: center;
  justify-content: center;
  animation: moving 1s linear;
}

@keyframes moving {
  0% {
    width: 0%;
  }
  100% {
    width: 100%;
  }
}

.cloud1 {
  position: absolute;
  height: 2em;
  width: 2em;
}

.cloud2 {
  position: absolute;
  height: 2em;
  width: 2em;
  z-index: 3;
}

.letter {
  z-index: 2;
}

.title .letter {
}

@keyframes tilt {
  0% {
    transform: rotate(20deg);
  }
  100% {
    transform: rotate(0deg);
  }
}
/*
.letter0 {
  animation: seting 0.5s linear;
}

@keyframes seting {
  0% {
    transform: translateX(100px);
  }
  100% {
    transform: translateX(0);
  }
}

.letter1 {
  animation: seting 0.5s linear;
}

@keyframes seting {
  0% {
    transform: translateX(90px);
  }
  100% {
    transform: translateX(0);
  }
}
*/

.letter0 {
  opacity: 1;
  animation: moveto1 0.5s ease;
}
.letter1 {
  opacity: 1;
  animation: moveto2 0.5s ease;
}
.letter2 {
  opacity: 1;
  animation: moveto3 0.5s ease;
}
.letter3 {
  opacity: 1;
  animation: moveto4 0.5s ease;
}
.letter4 {
  opacity: 1;
  animation: moveto5 0.5s ease;
}
.letter5 {
  opacity: 1;
  animation: moveto6 0.5s ease;
}
.letter6 {
  opacity: 1;
  animation: moveto7 0.5s ease;
}
.letter7 {
  opacity: 1;
  animation: moveto7 0.5s ease;
}
.letter8 {
  opacity: 1;
  animation: moveto8 0.5s ease;
}
.letter9 {
  opacity: 1;
  animation: moveto9 0.5s ease;
}
.letter10 {
  opacity: 1;
  animation: moveto10 0.5s ease;
}

@keyframes moveto1 {
  0% {
    opacity: 0;
    transform: translateX(200px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto2 {
  0% {
    opacity: 0;
    transform: translateX(140px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto2 {
  0% {
    opacity: 0;
    transform: translateX(120px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
@keyframes moveto3 {
  0% {
    opacity: 0;
    transform: translateX(100px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
@keyframes moveto4 {
  0% {
    opacity: 0;
    transform: translateX(80px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto5 {
  0% {
    opacity: 0;
    transform: translateX(20px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto6 {
  0% {
    opacity: 0;
    transform: translateX(0px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto7 {
  0% {
    opacity: 0;
    transform: translateX(-60px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto8 {
  0% {
    opacity: 0;
    transform: translateX(-120px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto9 {
  0% {
    opacity: 0;
    transform: translateX(-150px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes moveto10 {
  0% {
    opacity: 0;
    transform: translateX(-180px);
  }
  100% {
    opacity: 1;
    transform: translateX(0);
  }
}
</style>
