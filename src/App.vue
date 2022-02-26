<template>
  <h4 id="round-counter" v-if="gameState === 'playing'">
    Round: {{ roundsInPlay }}
  </h4>

  <Home v-if="gameState === 'initial'" :play="play" @rounds="setRounds" />
  <Block
    v-if="gameState === 'playing'"
    :delay="delay"
    @end="endRound"
    :key="times"
  />
  <Results
    v-if="gameState === 'results'"
    :score="score"
    @playAgain="returnToInitial"
  />
</template>

<script setup lang="ts">
import Home from "./components/Home.vue";
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
import { ref } from "vue";

export type gameState = "initial" | "playing" | "results";

const gameState = ref<gameState>("initial");
const delay = ref(0);
const score = ref(0);
const times = ref(0);
const roundsInPlay = ref(1);
let gameRounds = 1;

function setRounds(rounds: number) {
  gameRounds = rounds;
  roundsInPlay.value = rounds;
}

function play() {
  gameState.value = "playing";
  delay.value = 500 + Math.random() * 1500;
}

function endRound(reactionTime: number) {
  times.value += reactionTime;
  roundsInPlay.value--;
  if (roundsInPlay.value > 0) play();
  else endGame(times.value / gameRounds);
}

function endGame(final: number) {
  score.value = final;
  gameState.value = "results";
}

function returnToInitial() {
  delay.value = 0;
  score.value = 0;
  times.value = 0;
  roundsInPlay.value = 1;
  gameRounds = 1;
  gameState.value = "initial";
}
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 62.5%;
  text-align: center;

  color: #fff;
  background-color: #2c3e50;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 0;
  width: 100%;
  min-height: 100vh;
}

#round-counter {
  position: absolute;
  top: 0;
  font-size: 2.5rem;
}
</style>
