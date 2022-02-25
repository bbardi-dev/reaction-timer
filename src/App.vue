<template>
  <Main :play="play" :isPlaying="isPlaying" />
  <!-- <Results :score="score" />
  <Block v-if="isPlaying" :delay="delay" @end="endGame" /> -->
</template>

<script setup lang="ts">
import Main from "./components/Main.vue";
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";
import { ref } from "vue";

const isPlaying = ref(false);
const delay = ref(0);
const score = ref(0);

function play() {
  console.log("PLAYED");
  score.value = 0;
  isPlaying.value = true;
  delay.value = 500 + Math.random() * 1500;
}

function endGame(reactionTime: number) {
  score.value = reactionTime;
  isPlaying.value = false;
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
}
</style>
