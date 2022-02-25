<template>
  <Home v-if="isPlaying === 'initial'" :play="play" />
  <Block v-if="isPlaying === 'playing'" :delay="delay" @end="endGame" />
  <Results
    v-if="isPlaying === 'results'"
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

const isPlaying = ref<gameState>("initial");
const delay = ref(0);
const score = ref(0);

function play() {
  score.value = 0;
  isPlaying.value = "playing";
  delay.value = 500 + Math.random() * 1500;
}

function endGame(reactionTime: number) {
  score.value = reactionTime;
  isPlaying.value = "results";
}

function returnToInitial() {
  isPlaying.value = "initial";
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 62.5%;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  padding: 0;
  width: 100%;
  min-height: 90vh;
}
</style>
