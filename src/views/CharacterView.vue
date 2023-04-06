<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

let data = ref('')

onMounted(async () => {
  const response = await axios.get('https://rickandmortyapi.com/api/character')
  data.value = response.data.results
})

let search = ref('')
let searchResult = ref([])
let searchCharacter = () => {
  searchResult.value = data.value.filter((item) => {
    return item.name.toLowerCase().includes(search.value.toLowerCase())
  })
  data.value = searchResult.value
}

let page = ref(1)
let previousPage = () => {
  page.value--
  axios.get(`https://rickandmortyapi.com/api/character?page=${page.value}`)
    .then(response => {
      data.value = response.data.results
    })
}
let nextPage = () => {
  page.value++
  axios.get(`https://rickandmortyapi.com/api/character?page=${page.value}`)
    .then(response => {
      data.value = response.data.results
    })
}

let status = ref('')
let statusResult = ref([])
let statusCharacter = () => {
  statusResult.value = data.value.filter((item) => {
    return item.status.toLowerCase().includes(status.value.toLowerCase())
  })
  data.value = statusResult.value
}

</script>


<template>

<div id="recherche">
      <div id="pagination">
        <button @click="previousPage">Page précédente</button>
        <button @click="nextPage">Page suivante</button>
      </div>
    <label for="recherche">Rechercher par nom</label>
    <input type="text" id="recherche" v-model="search" placeholder="ex : Morty">
    <button @click="searchCharacter">Rechercher</button>
    <hr>

</div>

<div id="filtre">
    <label for="status">Filtrer les personnages par status</label>
    <select name="status" id="status" v-model="status">
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button @click="statusCharacter">Filtrer</button>
    <hr>
</div>

  <div id="app">
    <div class="grid-container">
      <div v-for="item in data" :key="item.id" class="grid-item">
        <img :src="item.image" alt="image" />
        <p>{{ item.name }}</p>
        <router-link :to="{ name: 'details', params: { id: item.id } }">  
          <p>Plus d'infos</p>
        </router-link>
      </div>
    </div>
  </div>
</template>



<style>

#app {
  display: flex;
  justify-content: center;
}

#recherche {
  display: flex;
  justify-content: center;
}

#pagination {
  margin-right: 30px;
  margin: 5px;
}

#recherche input {
  margin-right: 10px;
}

#recherche label {
  margin-right: 10px;
}

#filtre {
  display: flex;
  justify-content: center;
  margin-top: 20px;
}

#filtre label {
  margin-right: 10px;
}

#filtre select {
  margin-right: 10px;
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

