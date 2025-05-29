<template>
  <div class="game-container">
    <h1>Is it #000000?</h1>
    
    <div 
      v-if="!gameOver"
      class="color-display"
      :style="{ backgroundColor: currentColor }"
    ></div>
    
    <div v-if="!gameOver" class="button-container">
      <button @click="checkAnswer(true)" class="answer-btn yes">Yes</button>
      <button @click="checkAnswer(false)" class="answer-btn no">No</button>
    </div>
    
    <div v-else class="game-over">
      <h2>Game Over!</h2>
      <p>Your score: {{ score }}/10</p>
      <button @click="resetGame" class="reset-btn">Play Again</button>
    </div>
    
    <div class="progress">
      Round: {{ currentRound }}/10
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue';

const currentRound = ref(1);
const score = ref(0);
const gameOver = ref(false);
const currentColor = ref('');
const isBlack = ref(false);

// Generate a random dark color close to black
const generateDarkColor = (): { color: string, isBlack: boolean } => {
  // 20% chance to generate true black
  if (Math.random() < 0.3 && currentRound.value <= 7) { // Ensure we don't go over 3 true blacks
    return { color: '#000000', isBlack: true };
  }
  
  // Generate a very dark gray
  const darkValue = Math.floor(Math.random() * 30); // 0-29 for dark grays
  const hex = darkValue.toString(16).padStart(2, '0');
  return { 
    color: `#${hex}${hex}${hex}`, 
    isBlack: false 
  };
};

const nextRound = () => {
  if (currentRound.value >= 10) {
    gameOver.value = true;
    return;
  }
  
  currentRound.value++;
  const { color, isBlack: isBlackColor } = generateDarkColor();
  currentColor.value = color;
  isBlack.value = isBlackColor;
};

const checkAnswer = (userAnswer: boolean) => {
  if (userAnswer === isBlack.value) {
    score.value++;
  }
  nextRound();
};

const resetGame = () => {
  currentRound.value = 1;
  score.value = 0;
  gameOver.value = false;
  const { color, isBlack: isBlackColor } = generateDarkColor();
  currentColor.value = color;
  isBlack.value = isBlackColor;
};

// Initialize game
onMounted(() => {
  const { color, isBlack: isBlackColor } = generateDarkColor();
  currentColor.value = color;
  isBlack.value = isBlackColor;
});
</script>

<style scoped>
.game-container {
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
  padding: 1rem;
  text-align: center;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  padding-bottom: 2rem;
  position: relative;
}

h1 {
  font-size: clamp(1.5rem, 6vw, 2.5rem);
  margin: 0.5em 0 0.25em;
  line-height: 1.2;
  padding: 0 0.5rem;
}

.color-display {
  width: var(--color-display-size, min(80vw, 280px));
  height: var(--color-display-size, min(80vw, 280px));
  margin: 1rem auto;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  touch-action: manipulation;
  flex-shrink: 0;
}

.button-container {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  margin: 1rem auto;
  width: 100%;
  max-width: 280px;
  padding: 0 0.5rem;
  box-sizing: border-box;
}

.answer-btn {
  padding: 1rem;
  font-size: 1.1rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
  transition: transform 0.1s, opacity 0.2s;
  width: 100%;
  -webkit-tap-highlight-color: transparent;
  touch-action: manipulation;
  user-select: none;
}

.answer-btn:active {
  transform: scale(0.98);
}

.yes {
  background-color: #4CAF50;
  color: white;
}

.no {
  background-color: #f44336;
  color: white;
}

.reset-btn {
  padding: 1rem 2rem;
  font-size: 1.1rem;
  background-color: #2196F3;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  margin-top: 1.5rem;
  width: 100%;
  max-width: 300px;
  -webkit-tap-highlight-color: transparent;
  touch-action: manipulation;
}

.progress {
  font-size: 1.1rem;
  color: #aaa;
  padding: 0.5rem;
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(51, 51, 51, 0.9);
  z-index: 10;
}

.game-over h2 {
  color: #2196F3;
  margin-bottom: 1rem;
  font-size: 1.8rem;
}

.game-over p {
  font-size: 1.4rem;
  margin: 1rem 0;
}

/* Landscape mode adjustments */
@media (min-width: 600px) {
  .button-container {
    flex-direction: row;
    max-width: 100%;
  }
  
  .answer-btn {
    padding: 0.8rem 1.5rem;
    width: auto;
    flex: 1;
  }
  
  .reset-btn {
    max-width: 300px;
  }
}

/* Prevent text selection on buttons */
button {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* Better touch targets for mobile */
@media (max-width: 480px) {
  .answer-btn, .reset-btn {
    padding: 1.2rem;
    font-size: 1.2rem;
  }
  
  .progress {
    font-size: 1rem;
  }
}
</style>
