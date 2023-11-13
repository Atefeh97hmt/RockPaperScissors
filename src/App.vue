<script setup>
import { ref, watchEffect, computed } from "vue";
const userChoice = ref();
const computerChoice = ref();
const userScore = ref(0);
const computerScore = ref(0);
const rocks = ref("rocks");
const scissors = ref("scissors");
const paper = ref("paper");
const counter = ref(0);

// This function is called when the user clicks on one of the buttons to choose Rock, Paper, or Scissors. The function updates userChoice and computerChoice based on the user's selection and increments the computerScore if the user loses.
const choose = (pick) => {
  userChoice.value = pick;
  if (userChoice.value === rocks.value) {
    computerChoice.value = paper.value;
    computerScore.value++;
  } else if (userChoice.value === scissors.value) {
    computerChoice.value = rocks.value;
    computerScore.value++;
  } else if (userChoice.value === paper.value) {
    computerChoice.value = scissors.value;
    computerScore.value++;
  }
};

// This watchEffect is used to increment the counter variable every second, simulating a timer. The timer is used to display the elapsed time in hours, minutes, and seconds.
watchEffect(() => {
  if (counter.value >= 0) {
    setTimeout(() => {
      counter.value++;
    }, 1000);
  }
});

const hours = computed(() => Math.floor(counter.value / 60 / 60));
const minutes = computed(() => Math.floor((counter.value / 60) % 60));
const seconds = computed(() => Math.floor(counter.value % 60));
</script>

<template>
  <div class="game-container">
    <h1 class="game-title">Rock Paper Scissors</h1>
    <div class="button-container">
      <button @click="choose('rocks')">Rocks</button>
      <button @click="choose('paper')">Paper</button>
      <button @click="choose('scissors')">Scissors</button>
    </div>
    <h1 class="score">User({{ userScore }}) - Computer({{ computerScore }})</h1>
    <p class="timer">{{ hours }} : {{ minutes }} : {{ seconds }}</p>
  </div>
</template>

<style scoped>
.game-container {
  text-align: center;
  margin-top: 150px;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.game-title {
  color: cadetblue;
  font-weight: bold;
}

.button-container {
  justify-content: space-between;
  width: 100%;
  margin-top: 10px;
  margin: 5px 0;
}

button {
  padding: 0.8rem;
  margin: 20px 2px;
}

.score {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 15px;
}

.timer {
  font-size: 25px;
  font-weight: bold;
  width: 150px;
  background-color: thistle;
  text-align: center;
}
</style>
