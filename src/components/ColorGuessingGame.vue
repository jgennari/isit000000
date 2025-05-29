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
  max-width: 500px;
  margin: 0 auto;
  padding: 2rem;
  text-align: center;
}

.color-display {
  width: 300px;
  height: 300px;
  margin: 2rem auto;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin: 1rem 0;
}

.answer-btn {
  padding: 0.8rem 2rem;
  font-size: 1.1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
  transition: transform 0.1s, opacity 0.2s;
}

.answer-btn:active {
  transform: scale(0.95);
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
  padding: 0.8rem 2rem;
  font-size: 1.1rem;
  background-color: #2196F3;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 1rem;
}

.progress {
  margin-top: 2rem;
  font-size: 1.2rem;
  color: #666;
}

.game-over h2 {
  color: #2196F3;
  margin-bottom: 1rem;
}

game-over p {
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
}
</style>
