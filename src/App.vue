<script lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <h1 class="green align--center header--style">Welcome to Jokes page!</h1>
    </div>
    <div class="align--center">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/favorites">Favorites</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView />
</template>

<style scoped></style>
