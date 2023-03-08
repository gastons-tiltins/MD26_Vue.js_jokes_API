<script lang="ts">
import axios from 'axios'
// import type { FavJokes } from './HomeView.vue'

interface FavJokes {
  _id: string
  joke: string
  fav: boolean
}

export default {
  data() {
    return {
      favData: [] as FavJokes[]
    }
  },
  mounted() {
    axios
      .get('http://localhost:3004/jokes')
      .then((response) => {
        this.favData = response.data
      })
      .catch((error) => {
        error.message
      })
  }
}
</script>
<template>
  <div>
    <h1>FAVORITES</h1>
    <!-- <p>{{ favData }}</p> -->
    <div>
      <ul>
        <li v-for="joke in favData" :key="joke._id">
          {{ joke.joke }}
          <!-- <button @click="handleClick(joke.joke)">Add to favorites</button> -->
        </li>
      </ul>
      <hr />
    </div>
  </div>
</template>

<style></style>
