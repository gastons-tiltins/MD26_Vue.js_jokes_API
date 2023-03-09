<script lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <h1 class="green is-size-3 has-text-centered has-text-weight-bold">Welcome to Jokes page!</h1>
    </div>
    <div class="is-size-5 has-text-centered">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/favorites">Favorites</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView />
</template>

<style scoped></style>
