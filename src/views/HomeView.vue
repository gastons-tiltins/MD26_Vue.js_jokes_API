<script lang="ts">
import axios from 'axios'
import TestStuff from './TestStuff.vue'

export interface Jokes {
  category: string
  type: string
  joke: string
  flags: {
    nsfw: boolean
    religious: boolean
    political: boolean
    racist: boolean
    sexist: boolean
    explicit: boolean
  }
  id: number
  error?: boolean
  amount?: number
}

interface FavJokes {
  _id: string
  joke: string
  fav: boolean
}

export default {
  data() {
    return {
      jokesData: [] as Jokes[],
      favData: [] as FavJokes[]
    }
  },
  mounted() {
    axios
      .get('https://v2.jokeapi.dev/joke/Programming?type=single&amount=10')
      .then((response) => {
        this.jokesData = response.data.jokes
      })
      .catch((error) => {
        error.message
      })

    axios
      .get('http://localhost:3004/jokes')
      .then((response) => {
        this.favData = response.data
      })
      .catch((error) => {
        error.message
      })
  },
  methods: {
    handleClick(joke: string) {
      console.log('Joke added to favorites!')
      axios.post('http://localhost:3004/jokes', { joke, fav: true })
    }
  }
}
</script>
<template>
  <div>
    <h1>HOME</h1>
    <!-- {{ jokesData }} -->
    <p>{{ favData }}</p>
    <ul>
      <li v-for="joke in jokesData" :key="joke.id">
        {{ joke.joke }}
        <button @click="handleClick(joke.joke)">Add to favorites</button>
      </li>
    </ul>
    <hr />
  </div>
</template>
<style></style>
