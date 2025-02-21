<template>
  <div class="city-card">
    <div class="half top border-bottom">
      <div class="info">
        <div class="city-name">Stockholm</div>
        <div class="main-temperature">44°</div>
        <div class="wind-container">
          <div class="wind-name">Wind</div>
          <div class="wind-value">20km/h</div>
        </div>
        <div class="wind-container">
          <div class="wind-name">Humidity</div>
          <div class="wind-value">70%</div>
        </div>
      </div>
      <div class="icon">
        <Clouds></Clouds>
      </div>
    </div>
    <div class="half-bottom days daysfade" ref="daysref">
      <div class="day">
        <div>Now</div>
        <div class="day-icon"><Sun></Sun></div>
        <div>44°</div>
      </div>
      <div class="day">
        <div>16:00</div>
        <div class="day-icon"><Sun></Sun></div>
        <div>44°</div>
      </div>
      <div class="day">
        <div>17:00</div>
        <div class="day-icon"><Sun></Sun></div>
        <div>44°</div>
      </div>
      <div class="day">
        <div>18:00</div>
        <div class="day-icon"><Sun></Sun></div>
        <div>44°</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.days::-webkit-scrollbar {
  height: 3px;
}

.days::-webkit-scrollbar-button {
  display: none;
}

.days::-webkit-scrollbar-thumb {
  background-color: #000000;
  border-radius: 5px;
}

.days::-webkit-scrollbar-track {
  background-color: rgb(255, 255, 255);
}

.daysfade {
  -webkit-mask-image: linear-gradient(90deg, #020202 90%, transparent);
}

.days {
  display: flex;
  flex-direction: row;
  align-items: start;
  justify-content: start;
  gap: 10px;
  padding-top: 10px;
  width: 100%;
  overflow-x: scroll;
  padding-bottom: 5px;
  position: relative;
}

.day {
  border: 1px solid black;
  border-radius: 10px;
  box-sizing: border-box;
  padding-top: 10px;
  padding-bottom: 10px;
  min-width: 100px;
  max-width: 100px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: start;
  align-items: center;
  gap: 10px;
}

.day-icon {
  display: flex;
  justify-content: start;
  align-items: center;
  width: 50%;
  height: 40%;
}

.city-name {
  font-size: 1.5em;
}

.main-temperature {
  font-size: 2.5em;
  font-weight: bold;
}

.wind-name {
  width: 50%;
}

.wind-value {
  width: 50%;
  display: flex;
  align-items: end;
  justify-content: end;
}

.wind-container {
  display: flex;
  flex-direction: row;
  width: 100%;
}

.info {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
}

.icon {
  border: 1px solid black;
  border-radius: 10px;
  height: 100%;
  width: 60%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.top {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding-bottom: 10px;
}

.half {
  width: 100%;
  height: 50%;
}

.half-bottom {
  width: 100%;
}

.border-bottom {
  border-bottom: 1px solid black;
  width: 95%;
}

.city-card {
  border: 3px solid black;
  border-radius: 20px;
  width: 300px;
  height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.2);
  transition: transform 0.2s ease;
  background-color: white;
  padding: 10px;
}

.city-card:hover {
  transform: scale(1.1);
}
</style>
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Snowing from './components/Snowing.vue'
import Wind from './components/icons/Wind.vue'
import Raining from './components/icons/Raining.vue'
import Sun from './components/icons/Sun.vue'
import Clouds from './components/Clouds.vue'

const daysref = ref(null)

onMounted(() => {
  const container = daysref.value
  console.log(container)

  container.addEventListener('scroll', () => {
    if ((container.scrollLeft + container.clientWidth) * 1.1 >= container.scrollWidth) {
      console.log('Reached the right end!')
      container.classList.remove('daysfade')
    } else {
      container.classList.add('daysfade')
    }
  })
})
</script>
