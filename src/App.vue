<template>
  <h1>Simple Reaction Timer</h1>
  <button @click="play" :disabled="isPlaying">Play</button>
  <p v-if="score">Reaction Time: ~{{ score }}ms</p>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
</template>

<script lang="ts">
import Block from "./components/Block.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  components: { Block },
  data() {
    return {
      isPlaying: false,
      delay: 0,
      score: 0,
    };
  },
  methods: {
    play() {
      this.score = 0;
      this.isPlaying = true;
      this.delay = 100 + Math.random() * 4000;
    },
    endGame(reactionTime: number) {
      this.score = reactionTime;
      this.isPlaying = false;
    },
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
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
