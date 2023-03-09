<script lang="ts">
import axios from 'axios'

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
  id?: number
  joke: string
}

interface Result {
  _id?: number | undefined
  joke: string
}

export default {
  data() {
    return {
      jokesData: [] as Jokes[],
      favData: [] as FavJokes[],
      favJokes: [] as string[],
      firstImageSrc: 'fav-unselected.png',
      secondImageSrc: 'fav-selected.png'
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
        this.favData.forEach((joke) => {
          this.favJokes.push(joke.joke)
        })
      })
      .catch((error) => {
        error.message
      })
  },
  methods: {
    handleAddFav(joke: string) {
      axios.post('http://localhost:3004/jokes', { joke }).then((response) => {
        axios
          .get('http://localhost:3004/jokes')
          .then((response) => {
            this.favData = response.data
          })
          .catch((error) => {
            error.message
          })
      })
      this.favJokes = [...this.favJokes, joke]
      console.log('Joke added to favorites!')
    },
    handleDelete(joke: string) {
      const jokeValueToFind = joke
      const result: Result = this.favData.find((item) => item.joke === jokeValueToFind)!
      axios.delete(`http://localhost:3004/jokes/${result._id}`)
      let index = this.favJokes.indexOf(joke)
      if (index !== -1) {
        this.favJokes.splice(index, 1)
      }
    }
  }
}
</script>
<template>
  <div>
    <h1 class="is-size-4 has-text-centered">Home</h1>
    <div>
      <div v-for="joke in jokesData" :key="joke.id" class="apply--flex">
        <img
          v-if="!favJokes.includes(joke.joke)"
          :src="firstImageSrc"
          style="width: 20px; height: auto; cursor: pointer"
          alt="Favorite unselected."
          @click="handleAddFav(joke.joke)"
        />
        <img
          v-if="favJokes.includes(joke.joke)"
          :src="secondImageSrc"
          style="width: 20px; height: auto; cursor: pointer"
          alt="Favorite unselected."
          @click="handleDelete(joke.joke)"
        />
        <span>{{ joke.joke }}</span>
      </div>
    </div>
    <hr />
  </div>
</template>
<style></style>
