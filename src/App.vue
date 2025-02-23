<script setup>
import Searchbar from './components/Searchbar.vue'
import CityCard from './components/CityCard.vue'
import { ref, onMounted } from 'vue'
import draggable from 'vuedraggable'
import { fetchWeatherApi } from 'openmeteo'
import CustomTitle from './components/CustomTitle.vue'

const cards = ref([])

const searchCity = ref(null)
const searchCityBorder = ref(false)
const searchCityBorder2 = ref(false)

function removeCity(event) {
  cards.value = cards.value.filter((c) => c.id !== event.id)
  localStorage.setItem('cities', JSON.stringify({ ...cards.value }))
}

function addToCity(event) {
  cards.value.push({ ...event, saved: true })
  cards.value.reverse()
  localStorage.setItem('cities', JSON.stringify({ ...cards.value }))

  searchCity.value = null
  searchCityBorder.value = false
  searchCityBorder2.value = false
}

async function loadCities() {
  const storedCity = localStorage.getItem('cities')
  if (storedCity) {
    try {
      let cities = JSON.parse(storedCity)
      for (let c in cities) {
        c = await getWeatherForCity(cities[c])
        cards.value.push({ ...c, saved: true })
      }
    } catch (e) {
      // If parsing fails, keep default values

      cards.value = []
    }
  }
}

onMounted(() => {
  loadCities()
  if (cards.value.length === 0) {
    const stockholm = {
      id: 2673730,
      name: 'Stockholm',
      lat: 59.32938,
      long: 18.06871,
      country_code: 'SE',
      country: 'Sweden',
      saved: true,
      latitude: 59.32938,
      longitude: 18.06871,
    }
    showCity(stockholm)
  }
})

async function getWeatherForCity(city) {
  const params = {
    latitude: city.latitude,
    longitude: city.longitude,
    hourly: [
      'temperature_2m',
      'relative_humidity_2m',
      'apparent_temperature',
      'precipitation_probability',
      'rain',
      'snowfall',
      'weather_code',
      'cloud_cover',
      'wind_speed_10m',
    ],
  }

  const url = 'https://api.open-meteo.com/v1/forecast'
  let responses = await fetchWeatherApi(url, params)

  // Helper function to form time ranges
  const range = (start, stop, step) =>
    Array.from({ length: (stop - start) / step }, (_, i) => start + i * step)

  // Process first location. Add a for-loop for multiple locations or weather models
  const response = responses[0]

  // Attributes for timezone and location
  const utcOffsetSeconds = response.utcOffsetSeconds()
  const timezone = response.timezone()
  const timezoneAbbreviation = response.timezoneAbbreviation()
  const latitude = response.latitude()
  const longitude = response.longitude()

  const hourly = response.hourly()

  // Note: The order of weather variables in the URL query and the indices below need to match!
  const weatherData = {
    hourly: {
      time: range(Number(hourly.time()), Number(hourly.timeEnd()), hourly.interval()).map(
        (t) => new Date((t + utcOffsetSeconds) * 1000),
      ),
      temperature2m: hourly.variables(0).valuesArray(),
      relativeHumidity2m: hourly.variables(1).valuesArray(),
      apparentTemperature: hourly.variables(2).valuesArray(),
      precipitationProbability: hourly.variables(3).valuesArray(),
      rain: hourly.variables(4).valuesArray(),
      snowfall: hourly.variables(5).valuesArray(),
      weatherCode: hourly.variables(6).valuesArray(),
      cloudCover: hourly.variables(7).valuesArray(),
      windSpeed10m: hourly.variables(8).valuesArray(),
    },
  }

  return { ...city, weather: weatherData }
}

async function showCity(event) {
  let city = { ...event, latitude: event.lat, longitude: event.long }
  let res = await getWeatherForCity(city)
  searchCity.value = { ...res }

  searchCityBorder.value = true
  searchCityBorder2.value = true
  return res
}

//TODO
// load page with initial city as berlin into first card
// complete search bar with api to show cities and get the return from clicking on it
</script>

<template>
  <main>
    <CustomTitle></CustomTitle>
    <Searchbar @show="showCity"></Searchbar>
    <Transition name="searchresultscard">
      <div class="searchResults" v-if="searchCityBorder2">
        <CityCard :city="searchCity" @save="addToCity"></CityCard>
      </div>
    </Transition>
    <Transition name="searchborderbar">
      <div v-if="searchCityBorder" class="searchBorder"></div>
    </Transition>
    <draggable
      class="list"
      :list="cards"
      easing="cubic-bezier(1, 0, 0, 1)"
      itemKey="'id'"
      handle=".corner"
      @start="dragging = true"
      @end="dragging = false"
    >
      <template #item="{ element }">
        <CityCard
          class="fade-in-card"
          v-bind:key="element.id"
          :city="element"
          @remove="removeCity"
        />
      </template>
    </draggable>
  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:ital,opsz,wght@0,6..12,200..1000;1,6..12,200..1000&display=swap');

body {
  margin: 0;
  padding: 0;
  padding-bottom: 3em;
}

main {
  font-family: 'Nunito Sans', serif;
  background-color: white;
  color: black;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 30px;
}

.list {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 30px;
}

.searchResults {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.searchBorder {
  padding-bottom: 30px;
  border-bottom: 1px solid black;
  width: 60%;
}

.fade-in-card {
  animation: fade 0.5s ease-in;
}

@keyframes fade {
  0% {
    transform: scale(0);
    opacity: 0;
  }
  100% {
    transform: scale(1);
    opacity: 1;
  }
}

.searchresultscard-enter-active {
  opacity: 0;
  transform: scale(0);
  transition:
    transform 0.5s ease,
    opacity 0.5s ease;
}

.searchresultscard-enter-to {
  transform: scale(1);
  opacity: 1;
}

.searchresultscard-leave-active {
  opacity: 1;
  transform: scale(1);
  transition:
    transform 0.5s ease,
    opacity 0.5s ease;
}

.searchresultscard-leave-to {
  transform: scale(0);
  opacity: 0;
}

.searchborderbar-enter-active {
  width: 0%;
  transition: width 0.5s ease;
}

.searchborderbar-enter-to {
  width: 60%;
}

.searchborderbar-leave-active {
  transition: width 0.5s ease;
}

.searchborderbar-leave-to {
  width: 0%;
}
</style>
