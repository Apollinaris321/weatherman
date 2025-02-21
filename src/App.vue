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

const cards = ref([{ id: 1 }, { id: 2 }, { id: 3 }, { id: 4 }])
</script>

<template>
  <main>
    <h1>Weatherman</h1>
    <Searchbar></Searchbar>
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
