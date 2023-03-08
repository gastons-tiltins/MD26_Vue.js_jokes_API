<script lang="ts">
export default {
  data() {
    return {
      text: 'Hover over me',
      showButton: false
    }
  },
  methods: {
    onButtonClick() {
      console.log('Button clicked')
    }
  }
}
</script>

<template>
  <div>
    <h1>TEST</h1>
    <p @mouseover="showButton = true" @mouseleave="showButton = false">
      {{ text }}
      <button v-if="showButton" @click="onButtonClick">Click me</button>
    </p>
  </div>
</template>
