<template>
  <div class="city-card">
    <div class="half top border-bottom">
      <div class="info">
        <div class="save-scale">
          <button class="save pressable-button" @click="bookmark">
            <BookmarkFill v-if="bookmarked" class="bookmark"></BookmarkFill>
            <Bookmark v-else class="bookmark"></Bookmark>
          </button>
        </div>

        <div class="main-info">
          <div class="text-info">
            <div class="city-name">{{ props.city?.name ? props.city?.name : 'Stockholm' }}</div>
            <div class="main-temperature">
              {{
                props.city?.weather.hourly.temperature2m[time_index].toFixed(0) == 0
                  ? 0
                  : props.city?.weather.hourly.temperature2m[time_index].toFixed(0)
              }}°
            </div>
          </div>

          <div class="icon">
            <Raining
              v-if="getWeatherStage(props.city?.weather.hourly.weatherCode[time_index]) === 'rain'"
            ></Raining>
            <Snowing
              v-else-if="
                getWeatherStage(props.city?.weather.hourly.weatherCode[time_index]) === 'snow'
              "
            ></Snowing>
            <Clouds
              v-else-if="
                getWeatherStage(props.city?.weather.hourly.weatherCode[time_index]) === 'cloudy'
              "
            ></Clouds>
            <Night v-else-if="nighttime"></Night>
            <Sun v-else></Sun>
          </div>
        </div>

        <div class="detail-info">
          <div class="wind-container">
            <div class="wind-name">Wind</div>
            <div class="wind-value">
              {{ props.city?.weather.hourly.windSpeed10m[time_index].toFixed(0) }} km/h
            </div>
          </div>
          <div class="wind-container">
            <div class="wind-name">Humidity</div>
            <div class="wind-value">
              {{ props.city?.weather.hourly.relativeHumidity2m[time_index].toFixed(0) }} %
            </div>
          </div>
          <div class="wind-container">
            <div class="wind-name">Chance of rain</div>
            <div class="wind-value">
              {{ props.city?.weather.hourly.relativeHumidity2m[time_index].toFixed(0) }} %
            </div>
          </div>
          <div class="wind-container">
            <div class="wind-name">Feels like</div>
            <div class="wind-value">
              {{ props.city?.weather.hourly.apparentTemperature[time_index].toFixed(0) }}°
            </div>
          </div>
        </div>
      </div>
    </div>
    <div
      class="half-bottom days daysfade"
      ref="daysref"
      @mousedown="startDrag"
      @mouseleave="stopDrag"
      @mouseup="stopDrag"
      @mousemove="doDrag"
    >
      <div class="day" v-for="d in days" :key="d.time">
        <div>{{ d.time === 'Now' ? 'Now' : d.time + ':00' }}</div>
        <div class="day-icon">
          <Raining v-if="getWeatherStage(d.code) === 'rain'"></Raining>
          <Snowing v-else-if="getWeatherStage(d.code) === 'snow'"></Snowing>
          <Clouds v-else-if="getWeatherStage(d.code) === 'cloudy'"></Clouds>
          <Night v-else-if="nighttime"></Night>
          <Sun v-else></Sun>
        </div>
        <div>{{ d.temp.toFixed(0) == 0 ? 0 : d.temp.toFixed(0) }}°</div>
      </div>
    </div>
    <div class="corner drag-handle"></div>
  </div>
</template>

<script setup>
import { ref, onMounted, computed, watch } from 'vue'
import Snowing from './Snowing.vue'
import Raining from './icons/Raining.vue'
import Sun from './icons/Sun.vue'
import Clouds from './Clouds.vue'
import Bookmark from './icons/Bookmark.vue'
import BookmarkFill from './icons/BookmarkFill.vue'
import Night from './icons/Night.vue'

const props = defineProps({
  city: {
    type: Object,
    // change this later to true
    required: false,
  },
})

const daysref = ref(null)

const temp = ref(0)

const time_index = ref(0)

// go 10 hours into the future for days forecast
const max_future_hours = 10

const days = ref([])
const nighttime = ref(false)

const bookmarked = ref(false)

watch(bookmarked, async (oldVal, newVal) => {
  if (bookmarked.value != props.city?.saved) {
    bookmarked.value = props.city?.saved
  }
})

const emit = defineEmits(['save', 'remove'])

function bookmark() {
  bookmarked.value = !bookmarked.value
  if (bookmarked.value) {
    emit('save', { ...props.city, saved: true })
  } else {
    emit('remove', { ...props.city, saved: false })
  }
}

function isNighttime() {
  const now = new Date() // Get the current date and time
  const currentHour = now.getHours() // Get the current hour (0-23)

  // Check if the current hour is between 21 (9 PM) and 5 (5 AM)
  return currentHour >= 21 || currentHour < 5
}

onMounted(() => {
  bookmarked.value = props.city?.saved

  nighttime.value = isNighttime()

  for (let i = 0; i < props.city?.weather.hourly.time.length; i++) {
    let res = isSameRoundedHour(props.city?.weather.hourly.time[i])

    if (res) {
      time_index.value = i
      days.value.push({
        time: 'Now',
        code: props.city?.weather.hourly.weatherCode[i + 1],
        temp: props.city?.weather.hourly.temperature2m[i + 1],
      })
      days.value.push({
        time: getHourFromISOString(props.city?.weather.hourly.time[i + 2]),
        code: props.city?.weather.hourly.weatherCode[i + 2],
        temp: props.city?.weather.hourly.temperature2m[i + 2],
      })
      days.value.push({
        time: getHourFromISOString(props.city?.weather.hourly.time[i + 3]),
        code: props.city?.weather.hourly.weatherCode[i + 3],
        temp: props.city?.weather.hourly.temperature2m[i + 3],
      })
      days.value.push({
        time: getHourFromISOString(props.city?.weather.hourly.time[i + 4]),
        code: props.city?.weather.hourly.weatherCode[i + 4],
        temp: props.city?.weather.hourly.temperature2m[i + 4],
      })
      days.value.push({
        time: getHourFromISOString(props.city?.weather.hourly.time[i + 5]),
        code: props.city?.weather.hourly.weatherCode[i + 5],
        temp: props.city?.weather.hourly.temperature2m[i + 5],
      })
      days.value.push({
        time: getHourFromISOString(props.city?.weather.hourly.time[i + 6]),
        code: props.city?.weather.hourly.weatherCode[i + 6],
        temp: props.city?.weather.hourly.temperature2m[i + 6],
      })
      days.value.push({
        time: getHourFromISOString(props.city?.weather.hourly.time[i + 7]),
        code: props.city?.weather.hourly.weatherCode[i + 7],
        temp: props.city?.weather.hourly.temperature2m[i + 7],
      })
      break
    }
  }

  temp.value = Math.floor(Math.random() * 10)
  const container = daysref.value

  container.addEventListener('scroll', () => {
    if ((container.scrollLeft + container.clientWidth) * 1.1 >= container.scrollWidth) {
      container.classList.remove('daysfade')
    } else {
      container.classList.add('daysfade')
    }
  })
})

function isSameRoundedHour(utcDateString) {
  const inputDate = new Date(utcDateString)

  const currentDate = new Date()

  const roundedInput = new Date(inputDate)
  roundedInput.setMinutes(0, 0, 0) // Reset minutes, seconds, milliseconds

  const roundedCurrent = new Date(currentDate)
  roundedCurrent.setMinutes(0, 0, 0)

  return (
    roundedInput.getFullYear() === roundedCurrent.getFullYear() &&
    roundedInput.getMonth() === roundedCurrent.getMonth() &&
    roundedInput.getDate() === roundedCurrent.getDate() &&
    roundedInput.getHours() === roundedCurrent.getHours()
  )
}

function getWeatherStage(weatherCode) {
  if (weatherCode === 0 || weatherCode === 1 || weatherCode === 2) return 'sunny'

  if ([3, 45, 48].includes(weatherCode)) return 'cloudy'

  if ([51, 53, 55, 56, 57, 61, 63, 65, 66, 67, 80, 81, 82, 95, 96, 99].includes(weatherCode)) {
    return 'rain'
  }

  if ([71, 73, 75, 77, 85, 86].includes(weatherCode)) return 'snow'

  return 'sunny'
}

function getHourFromISOString(isoString) {
  const date = new Date(isoString)
  return date.getUTCHours()
}

// Drag-to-scroll logic
let isDragging = false
let startX, scrollLeft

const startDrag = (e) => {
  isDragging = true
  startX = e.pageX - daysref.value.offsetLeft
  scrollLeft = daysref.value.scrollLeft
  daysref.value.style.cursor = 'grabbing' // Change cursor to grabbing
}

const stopDrag = () => {
  isDragging = false
  daysref.value.style.cursor = 'grab' // Reset cursor
}

const doDrag = (e) => {
  if (!isDragging) return
  e.preventDefault()
  const x = e.pageX - daysref.value.offsetLeft
  const walk = (x - startX) * 2 // Adjust multiplier for faster/slower scroll
  daysref.value.scrollLeft = scrollLeft - walk
}
</script>

<style scoped>
.city-card {
  position: relative;
  border: 0px solid black;
  border-radius: 20px;
  width: 350px;
  height: 440px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.15);
  transition: transform 0.2s ease;
  background-color: white;
  padding: 10px;
}

.city-card:hover {
  transform: scale(1.1);
}

.corner {
  position: absolute;
  border-right: 3px solid rgba(0, 0, 0, 25%);
  border-bottom: 3px solid rgba(0, 0, 0, 25%);
  border-bottom-right-radius: 20px;
  background-color: transparent;
  width: 8%;
  height: 8%;
  top: 92%;
  left: 92%;
  cursor: grab;
}

.corner:hover {
  border-right: 3px solid rgba(0, 0, 0);
  border-bottom: 3px solid rgba(0, 0, 0);
}

.days::-webkit-scrollbar {
  height: 8px;
  width: 1px !important;
}

.days::-webkit-scrollbar-button {
  display: none;
}

.days::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 0, 25%);
  opacity: 50%;
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
  padding-top: 15px;
  width: 100%;
  height: 40%;
  overflow-x: scroll;
  padding-bottom: 10px;
  position: relative;
  user-select: none;
}

.day {
  border: 0px solid black;
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
  transition: transform 0.2s ease;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.1);
}

.day-icon {
  display: flex;
  justify-content: start;
  align-items: center;
  width: 50%;
  height: 40%;
}

.day:hover {
  transform: scale(1.05);
}

.city-name {
  font-size: 2em;
}

.main-temperature {
  font-size: 2.5em;
  font-weight: bold;
}

.wind-name {
  width: 100%;
}

.wind-value {
  width: 40%;
  display: flex;
  align-items: start;
  justify-content: start;
}

.wind-container {
  display: flex;
  flex-direction: row;
  width: 100%;
}

/* Top half */

.info {
  height: 100%;
  width: 98%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: start;
}

.main-info {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  width: 100%;
  padding-bottom: 10px;
}

.detail-info {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.text-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100%;
}

.icon {
  border: 0px solid black;
  border-radius: 10px;
  height: 100%;
  width: 40%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.1);
  transition: transform 0.2s ease;
}

.top {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 10px;
  padding-bottom: 15px;
}

.half {
  width: 100%;
  height: 50%;
}

.half-bottom {
  width: 100%;
}

.border-bottom {
  border-bottom: 2px solid black;
  width: 95%;
}

.save {
  display: flex;
  padding: 4px;
  transform-origin: center;
  cursor: pointer;

  -webkit-user-select: none; /* Safari */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* IE10+/Edge */
  user-select: none;
}

.save:hover {
  /*
  animation: rotateShake 2s linear infinite;
  */
}

@keyframes rotateShake {
  0% {
    transform: rotate(0deg);
  }
  25% {
    transform: rotate(-10deg);
  }
  50% {
    transform: rotate(0deg);
  }
  75% {
    transform: rotate(10deg);
  }
  100% {
    transform: rotate(0deg);
  }
}

.save-scale {
  display: flex;
  justify-content: start;
  align-items: start;
  width: 100%;
}

.pressable-button {
  font-weight: bold;
  background-color: white;
  border: none;
  transition: transform 0.1s ease;
  box-shadow: 0.1s ease;
  cursor: pointer;
  border-radius: 50%;
  transition: transform 0.3s ease-in-out;
}

.pressable-button:hover {
  transform: scale(1.1);
}

.pressable-button:active {
  transform: scale(0.9); /* Scale down */
}

.bookmark {
  z-index: 10;
}
</style>
