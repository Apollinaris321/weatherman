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
        <ul v-show="isOpen" class="dropdown-menu" ref="dropdownRef">
          <li
            v-for="city in showResults"
            :key="city.id"
            class="menu-item"
            @click="selectOption(city)"
          >
            <div class="searchtext">{{ city.name }}, {{ city.country }}</div>
          </li>
        </ul>
      </transition>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import axios from 'axios'

const city = ref('')
const showResults = ref([])

const isOpen = ref(false)
const dropdownRef = ref(null)

const emit = defineEmits(['show'])

const selectOption = (option) => {
  for (let res of showResults.value) {
    if (res.id === option.id) {
      emit('show', { ...res })
    }
  }
  isOpen.value = false
  city.value = ''
}

async function logging(event) {
  let result_list = []
  if (city.value !== '' && city.value.length > 1) {
    let results = await axios.get(
      'https://geocoding-api.open-meteo.com/v1/search?name=' +
        city.value +
        '&count=10&language=en&format=json',
    )

    for (let res of results.data.results) {
      result_list.push({
        id: res.id,
        name: res.name,
        lat: res.latitude,
        long: res.longitude,
        country_code: res.country_code,
        country: res.country,
        saved: false,
      })
    }
  }

  showResults.value = [...result_list]

  if (showResults.value.length > 0) {
    isOpen.value = true
  } else {
    isOpen.value = false
  }
}

const handleClickOutside = (event) => {
  if (dropdownRef.value && !dropdownRef.value.contains(event.target)) {
    isOpen.value = false
    showResults.value = []
    city.value = ''
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
  align-items: center;
  width: 100%; /* adjust as needed */
  border-radius: 20px;
  box-shadow: 0 3px 10px rgb(0 0 0 / 0.1);
}

input {
  height: 30px;
  width: 100%;
  padding: 10px;
  padding-left: 20px;
  border: 0px solid black;
  border-right-width: 0px;
  border-top-left-radius: 20px;
  border-bottom-left-radius: 20px;
}

input:focus {
  border-right-width: 0px;
  outline: none;
}

.material-icons {
  border: 0px solid black;
  border-left-width: 0px;
  border-top-right-radius: 20px;
  border-bottom-right-radius: 20px;
  width: 10%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.magnify {
  width: 60%;
  height: 60%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.cont {
  position: relative;
  width: 30%;
  min-width: 300px;
  animation: start 0.6s ease;
}

@keyframes start {
  0% {
    opacity: 0;
    width: 0%;
  }
  50% {
  }
  100% {
    opacity: 100%;
    width: 30%;
  }
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

.searchtext {
  transition: transform 0.2s ease;
}

.searchtext:hover {
  transform: scale(1.05);
}
</style>
