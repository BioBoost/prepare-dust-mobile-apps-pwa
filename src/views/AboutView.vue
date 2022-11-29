<script setup lang="ts">
import axios from 'axios';
import { onMounted, ref } from 'vue';

const trees = ref([] as any);
const error = ref("");

const baseURL = import.meta.env.VITE_API_ENDPOINT || '/api'
const api = axios.create({
  baseURL: baseURL
})

onMounted(() => {
  api.get('/trees')
  .then((response) => {
    // console.log(response)
    trees.value = response.data.data;
  })
  .catch((err) => {
    // console.log("failed to get response");
    error.value = err.message;
  })
})

const envVar = import.meta.env.VITE_MY_ENV_VAR
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div>Environment variable: {{ envVar }}</div>
    <div>API EndPoint: {{ baseURL }}</div>

    <div>
      <h3>Trees</h3>
      <ul>
        <li v-for="tree in trees" :key="tree.id">{{ tree.name}}</li>
      </ul>
      <div>
        {{ error }}
      </div>
    </div>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}
</style>
