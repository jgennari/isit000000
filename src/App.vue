<script setup lang="ts">
import ColorGuessingGame from './components/ColorGuessingGame.vue';
</script>

<template>
  <div class="app">
    <ColorGuessingGame />
  </div>
</template>

<style>
:root {
  --max-content-width: 100%;
  --content-padding: 1rem;
  --color-display-size: min(80vw, 280px);
  
  @media (min-width: 600px) {
    --color-display-size: min(90vw, 400px);
  }
}

html, body {
  margin: 0;
  padding: 0;
  width: 100%;
  height: 100%;
  overflow-x: hidden;
  -webkit-text-size-adjust: 100%;
  -ms-text-size-adjust: 100%;
  touch-action: manipulation;
}

body {
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #333333;
  color: #ffffff;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  padding: 0;
  margin: 0;
}

.app {
  width: 100%;
  max-width: var(--max-content-width);
  margin: 0 auto;
  padding: var(--content-padding);
  text-align: center;
  box-sizing: border-box;
}

/* Prevent zoom on mobile devices when tapping buttons */
button, input, textarea, select {
  font-size: 16px;
  touch-action: manipulation;
}
</style>
