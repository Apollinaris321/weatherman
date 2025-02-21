<template>
  <div class="cont">
    <div class="input-container">
      <input v-model="city" @input="logging" type="text" placeholder="Search for a city..." />
      <div class="material-icons">
        <svg viewBox="0 0 24 24" class="magnify">
          <path
            d="M9.5,3A6.5,6.5 0 0,1 16,9.5C16,11.11 15.41,12.59 14.44,13.73L14.71,14H15.5L20.5,19L19,20.5L14,15.5V14.71L13.73,14.44C12.59,15.41 11.11,16 9.5,16A6.5,6.5 0 0,1 3,9.5A6.5,6.5 0 0,1 9.5,3M9.5,5C7,5 5,7 5,9.5C5,12 7,14 9.5,14C12,14 14,12 14,9.5C14,7 12,5 9.5,5Z"
          />
        </svg>
      </div>

      <transition name="fade">
        <ul v-show="isOpen" class="dropdown-menu">
          <li
            v-for="city in showResults"
            :key="city.id"
            class="menu-item"
            @click="selectOption(city)"
          >
            {{ city.name }}, {{ city.country }} {{ city.id }}
          </li>
        </ul>
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import axios from 'axios'

const response = ref('')
const cities = ref('')

onMounted(async () => {
  //""latitude": 51.1074, "longitude": 7.64838, "
  // let res = await axios.get(
  //   'https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&past_days=10&hourly=temperature_2m,relative_humidity_2m,wind_speed_10m',
  // )
  // let cities_res = await axios.get(
  //   'https://geocoding-api.open-meteo.com/v1/search?name=Meinerzhagen&count=10&language=en&format=json',
  // )
  //
  // let res = await axios.get(
  //   'https://api.open-meteo.com/v1/forecast?latitude=51.10&longitude=7.65&past_days=10&hourly=temperature_2m&forecast_days=1',
  // )
  /*
  const params = {
	"latitude": 50.9333,
	"longitude": 6.95,
	"hourly": ["temperature_2m", "relative_humidity_2m", "apparent_temperature", "precipitation_probability", "rain", "snowfall", "weather_code", "cloud_cover"]
  };
  const url = "https://api.open-meteo.com/v1/forecast";
  const responses = await fetchWeatherApi(url, params);

  */
  // https://geocoding-api.open-meteo.com/v1/search?name=58540&count=10&language=en&format=json
  // name
  //console.log(res.data)
  //response.value = res.data
  //cities.value = cities_res.data
})

const city = ref('')
const showResults = ref([])

const cities_list = ref([
  {
    id: 2950159,
    name: 'Berlin',
    latitude: 52.52437,
    longitude: 13.41053,
    elevation: 74,
    feature_code: 'PPLC',
    country_code: 'DE',
    admin1_id: 2950157,
    admin3_id: 6547383,
    admin4_id: 6547539,
    timezone: 'Europe/Berlin',
    population: 3426354,
    postcodes: ['10967', '13347'],
    country_id: 2921044,
    country: 'Germany',
    admin1: 'Land Berlin',
    admin3: 'Berlin, Stadt',
    admin4: 'Berlin',
  },
  {
    id: 3078610,
    name: 'Brno',
    latitude: 49.19522,
    longitude: 16.60796,
    elevation: 226,
    feature_code: 'PPLA',
    country_code: 'CZ',
    admin1_id: 3339536,
    admin2_id: 3078609,
    timezone: 'Europe/Prague',
    population: 369559,
    country_id: 3077311,
    country: 'Czechia',
    admin1: 'South Moravian',
    admin2: 'Město Brno',
  },
  {
    id: 64518,
    name: 'Beer',
    latitude: 9.36889,
    longitude: 45.74333,
    elevation: 927,
    feature_code: 'PPL',
    country_code: 'SO',
    admin1_id: 51230,
    timezone: 'Africa/Mogadishu',
    country_id: 51537,
    country: 'Somalia',
    admin1: 'Togdheer',
  },
  {
    id: 342363,
    name: 'Ber',
    latitude: 11.38333,
    longitude: 38.4,
    elevation: 2320,
    feature_code: 'PPL',
    country_code: 'ET',
    admin1_id: 444180,
    timezone: 'Africa/Addis_Ababa',
    country_id: 337996,
    country: 'Ethiopia',
    admin1: 'Amhara',
  },
  {
    id: 1182957,
    name: 'Landai',
    latitude: 31.35564,
    longitude: 70.17163,
    elevation: 693,
    feature_code: 'PPL',
    country_code: 'PK',
    admin1_id: 1183606,
    admin2_id: 6641955,
    timezone: 'Asia/Karachi',
    country_id: 1168579,
    country: 'Pakistan',
    admin1: 'Balochistan',
    admin2: 'Mūsa Khel',
  },
  {
    id: 1182958,
    name: 'Bir Sharif',
    latitude: 27.55914,
    longitude: 67.93607,
    elevation: 51,
    feature_code: 'PPL',
    country_code: 'PK',
    admin1_id: 1164807,
    admin2_id: 9034783,
    timezone: 'Asia/Karachi',
    country_id: 1168579,
    country: 'Pakistan',
    admin1: 'Sindh',
    admin2: 'Qamber Shahdadkot District',
  },
  {
    id: 1432207,
    name: 'Ber',
    latitude: 33.23187,
    longitude: 74.40381,
    elevation: 941,
    feature_code: 'PPL',
    country_code: 'IN',
    admin1_id: 1269320,
    timezone: 'Asia/Kolkata',
    country_id: 1269750,
    country: 'India',
    admin1: 'Jammu and Kashmir',
  },
  {
    id: 1479287,
    name: 'Ber',
    latitude: 35.00368,
    longitude: 72.85461,
    elevation: 1098,
    feature_code: 'PPL',
    country_code: 'PK',
    admin1_id: 1168873,
    admin2_id: 12105028,
    timezone: 'Asia/Karachi',
    country_id: 1168579,
    country: 'Pakistan',
    admin1: 'Khyber Pakhtunkhwa',
    admin2: 'Lower Kohistan District',
  },
  {
    id: 2099623,
    name: 'Ber',
    latitude: -9.16667,
    longitude: 142.26666,
    elevation: 11,
    feature_code: 'PPL',
    country_code: 'PG',
    timezone: 'Pacific/Port_Moresby',
    country_id: 2088628,
    country: 'Papua New Guinea',
  },
  {
    id: 2234382,
    name: 'Ber',
    latitude: 7.81667,
    longitude: 14.98333,
    elevation: 538,
    feature_code: 'PPL',
    country_code: 'CM',
    admin1_id: 2223603,
    timezone: 'Africa/Douala',
    country_id: 2233387,
    country: 'Cameroon',
    admin1: 'North',
  },
])

const isOpen = ref(false)
const dropdownRef = ref(null)

const emit = defineEmits(['show'])

const selectOption = (option) => {
  for (let res of cities_list.value) {
    if (res.id === option.id) {
      emit('show', { ...res })
    }
  }
  isOpen.value = false
  city.value = ''
}

async function logging(event) {
  let result_list = []
  // remove white spaces and only allow chars
  // the api only starts searching if the word is longer than one char
  let search = city.value.replace(' ', '')
  if (city.value !== '' && city.value.length > 1) {
    let results = await axios.get(
      'https://geocoding-api.open-meteo.com/v1/search?name=' +
        city.value +
        '&count=10&language=en&format=json',
    )

    // let res = await axios.get(
    //   'https://geocoding-api.open-meteo.com/v1/search?name=Berlin&count=10&language=en&format=json',
    // )
    console.log('results: ')
    console.log(city.value)
    console.log(results)

    //for (let res of results.data.results) {
    //for (let res of results) {
    for (let res of cities_list.value) {
      result_list.push({
        id: res.id,
        name: res.name,
        lat: res.latitude,
        long: res.longitude,
        country_code: res.country_code,
        country: res.country,
      })
    }
  }

  showResults.value = [...result_list]

  if (showResults.value.length > 0) {
    console.log('showing open suggestions')
    isOpen.value = true
  } else {
    isOpen.value = false
  }
}

const handleClickOutside = (event) => {
  if (dropdownRef.value && !dropdownRef.value.contains(event.target)) {
    isOpen.value = false
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>

<style scoped>
.input-container {
  display: flex;
  position: relative;
  align-items: stretch;
  width: 300px; /* adjust as needed */
}

input {
  height: 20px;
  width: 100%;
  padding: 10px;
  border: 3px solid black;
  border-right-width: 0px;
  border-top-left-radius: 1em;
  border-bottom-left-radius: 1em;
}

input:focus {
  border-right-width: 0px;
  outline: none;
}

.material-icons {
  border: 3px solid black;
  border-left-width: 0px;
  border-top-right-radius: 1em;
  border-bottom-right-radius: 1em;
  display: flex;
  justify-content: center;
  align-items: center;
}

.cont {
  position: relative;
}

.suggestions {
  list-style: none;
  padding: 0;
  margin: 0;
  border: 1px solid #ccc;
  border-top: none;
  position: absolute;
  width: 100%;
  background-color: #fff;
  max-height: 200px;
  overflow-y: auto;
  opacity: 0.1;
  z-index: 10;
}

.dropdown-container {
  position: relative;
  display: inline-block;
  font-family: Arial, sans-serif;
}

.dropdown-button {
  padding: 8px 16px;
  background-color: #ffffff;
  border: 1px solid #cccccc;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.dropdown-button:hover {
  background-color: #f5f5f5;
}

.dropdown-menu {
  position: absolute;
  width: 100%;
  opacity: 1;
  top: 100%;
  left: 0;
  margin-top: 4px;
  padding: 0;
  list-style: none;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  min-width: 100px;
  z-index: 1000;
}

.menu-item {
  padding: 8px 16px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.menu-item:hover {
  background-color: #f8f8f8;
}

.fade-enter-active,
.fade-leave-active {
  transition:
    opacity 0.2s,
    transform 0.2s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

.magnify {
  width: 30px;
  height: 30px;
}
</style>
