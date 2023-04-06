<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'
import { useRoute } from 'vue-router'

let data = ref('')

const route = useRoute()
let id = route.params.id

onMounted(async () => {
  const response = await axios.get(`https://rickandmortyapi.com/api/character/${id}`)
  data.value = response.data
})
</script>


<template>
  <div id="app">
    <div :key="data.id">
      <img :src="data.image" alt="image" />
      <div class="infos">
        <p id="name">{{ data.name }}</p>
        <p>Statut : {{ data.status }}</p>
        <p>Espèce : {{ data.species }}</p>
        <p>Genre : {{ data.gender }}</p>
        <p>Origine : {{ data.origin.name }}</p>
        <p>Dernière localisation : {{ data.location.name }}</p> 
      </div>
    </div>
  </div>
</template>

<style>

.infos {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  background-color: #333;
}

#name {
  font-size: 1.2rem;
  color: hsla(160, 100%, 37%, 1);
}

</style>



