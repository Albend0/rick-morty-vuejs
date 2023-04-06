<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

let data = ref('')

onMounted(async () => {
  const response = await axios.get('https://rickandmortyapi.com/api/episode')
  data.value = response.data.results
})

let search = ref('')
let searchResult = ref([])
let searchEpisode = () => {
  searchResult.value = data.value.filter((item) => {
    return item.name.toLowerCase().includes(search.value.toLowerCase())
  })
  data.value = searchResult.value
}

let page = ref(1)
let previousPage = () => {
  page.value--
  axios.get(`https://rickandmortyapi.com/api/episode?page=${page.value}`)
    .then(response => {
      data.value = response.data.results
    })
}
let nextPage = () => {
  page.value++
  axios.get(`https://rickandmortyapi.com/api/episode?page=${page.value}`)
    .then(response => {
      data.value = response.data.results
    })
}
</script>


<template>

<div id="recherche">
    <div id="pagination">
        <button @click="previousPage">Page précédente</button>
        <button @click="nextPage">Page suivante</button>
    </div>
    <label for="recherche">Rechercher un épisode</label>
    <input type="text" id="recherche" v-model="search" placeholder="Ex : Pilot">
    <button @click="searchEpisode">Rechercher</button>
    <hr>
</div>

  <div id="app">
    <div class="grid-container">
      <div v-for="item in data" :key="item.id" class="grid-item">
        <p>{{ item.name }}</p>
        <p>{{ item.episode }}</p>
        <p>{{ item.air_date }}</p>
      </div>
    </div>
  </div>
</template>


<style>

#app {
  display: flex;
  justify-content: center;
}

.grid-container {
  margin-top: 50px;
  display: grid;
  grid-template-columns: repeat(3, 1fr); 
  grid-gap: 10px;
}

.grid-item {
  border: 1px solid black;
  padding: 10px;
}

#carte {
  font-size: 40px;
}

</style>