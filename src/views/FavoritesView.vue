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
      favData: [] as FavJokes[],
      thirdImageSrc: 'delete.png'
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
  },
  methods: {
    handleDelete(_id: string) {
      axios.delete(`http://localhost:3004/jokes/${_id}`)
      this.favData = this.favData.filter((item) => item._id !== _id)
      console.log('Joke deleted from favorites!')
    }
  }
}
</script>
<template>
  <div>
    <h1 class="is-size-4 has-text-centered">Your Favorite Jokes</h1>
    <!-- <p>{{ favData }}</p> -->
    <div>
      <div v-for="joke in favData" :key="joke._id" class="apply--flex">
        <img
          @click="handleDelete(joke._id)"
          :src="thirdImageSrc"
          style="width: 20px; height: auto; cursor: pointer"
          alt="Favorite unselected."
        />
        <span>{{ joke.joke }}</span>
      </div>
      <hr />
    </div>
  </div>
</template>

<style></style>
