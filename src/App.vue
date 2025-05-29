<script setup lang="ts">
import ColorGuessingGame from './components/ColorGuessingGame.vue';
</script>

<template>
  <div class="app">
    <ColorGuessingGame />
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #333333;
  color: #ffffff;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.app {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}
</style>
