<script setup>
  import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div>
    <h1>TP Final</h1>
    <ul>
      <li><RouterLink to="/character">Les personnages</RouterLink></li>
      <li><RouterLink to="/episode">Les épisodes</RouterLink></li>
    </ul>
    <RouterView />
  </div>
</template>

<style scoped>

h1 {
  text-align: center;
}


ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-color: #333;
  text-align: center;
  margin-bottom: 20px;
}



</style>
