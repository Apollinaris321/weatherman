<script setup>
import Searchbar from './components/Searchbar.vue'
import CityCard from './CityCard.vue'
import CityCard2 from './CityCard2.vue'

import Snowing from './components/Snowing.vue'
import Wind from './components/icons/Wind.vue'
import Raining from './components/icons/Raining.vue'
import Sun from './components/icons/Sun.vue'
import Clouds from './components/Clouds.vue'
import { ref } from 'vue'
import draggable from 'vuedraggable'
import { fetchWeatherApi } from 'openmeteo'

const cards = ref([{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }])

async function showCity(event) {
  console.log('show this city: ', event)

  const params = {
    latitude: event.latitude,
    longitude: event.longitude,
    hourly: [
      'temperature_2m',
      'relative_humidity_2m',
      'apparent_temperature',
      'precipitation_probability',
      'rain',
      'snowfall',
      'weather_code',
      'cloud_cover',
    ],
  }
  const url = 'https://api.open-meteo.com/v1/forecast'
  const responses = await fetchWeatherApi(url, params)
  console.log('weather for the city of: ', event.name)

  // Helper function to form time ranges
  const range = (start, stop, step) =>
    Array.from({ length: (stop - start) / step }, (_, i) => start + i * step)

  // Process first location. Add a for-loop for multiple locations or weather models
  const response = responses[0]
  console.log(response)

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
    },
  }

  // `weatherData` now contains a simple structure with arrays for datetime and weather data
  for (let i = 0; i < weatherData.hourly.time.length; i++) {
    console.log(
      weatherData.hourly.time[i].toISOString(),
      weatherData.hourly.temperature2m[i],
      weatherData.hourly.relativeHumidity2m[i],
      weatherData.hourly.apparentTemperature[i],
      weatherData.hourly.precipitationProbability[i],
      weatherData.hourly.rain[i],
      weatherData.hourly.snowfall[i],
      weatherData.hourly.weatherCode[i],
      weatherData.hourly.cloudCover[i],
    )
  }
}

//TODO
// load page with initial city as berlin into first card
// complete search bar with api to show cities and get the return from clicking on it
</script>

<template>
  <main>
    <h1>Weatherman</h1>
    <Searchbar @show="showCity"></Searchbar>
    <draggable
      class="list"
      :list="cards"
      item-key="id"
      @start="dragging = true"
      @end="dragging = false"
    >
      <template #item="{ element }">
        <CityCard :key="element.id" />
      </template>
    </draggable>
  </main>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito+Sans:ital,opsz,wght@0,6..12,200..1000;1,6..12,200..1000&display=swap');

body {
  margin: 0;
  padding: 0;
  padding-top: 50px;
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
</style>
