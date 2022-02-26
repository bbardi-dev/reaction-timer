<template>
  <h2 v-if="score">Your Average Reaction Time: {{ score.toFixed(1) }}ms</h2>
  <p @click="playAgain">Play Again...</p>
</template>
<script setup lang="ts">
const props = defineProps<{ score: number }>();
const emit = defineEmits(["playAgain"]);

function playAgain() {
  emit("playAgain");
}
</script>

<style>
h2 {
  font-size: 2rem;
}

p {
  font-size: 1.25rem;
  font-weight: 600;
  color: #0faf87;
  cursor: pointer;
  text-decoration: underline;
}
</style>
