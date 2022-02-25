<template lang="">
  <div class="main">
    <h1>Simple Reaction Timer</h1>
    <button @click="play" :disabled="isPlaying">Play</button>
  </div>
</template>

<script setup lang="ts">
const props = defineProps<{ isPlaying: boolean; play: () => void }>();
</script>

<style>
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  width: 100%;
  min-height: 90vh;
}

h1 {
  font-size: 4rem;
}

button {
  border: none;
  background: #0faf87;
  color: #fff;
  font-weight: 500;
  font-size: 1.5rem;
  border-radius: 6px;
  text-align: center;
  letter-spacing: 0.05rem;
  padding: 0.5rem 4rem;
  cursor: pointer;
}
button:disabled {
  background: #af0f32;
}
</style>
