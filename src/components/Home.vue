<template lang="">
  <h1>Simple Reaction Timer</h1>
  <div id="menu">
    <button @click="play">Play</button>
    <span>Number of rounds:</span>
    <select @change="emission" v-model="rounds" name="rounds" id="rounds">
      <option v-for="option in options" :value="option">
        {{ option }}
      </option>
    </select>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const props = defineProps<{ play: () => void }>();
const rounds = ref("1");
const options = ref([1, 3, 5, 10, 15, 20, 30]);
const emit = defineEmits(["rounds"]);

function emission() {
  emit("rounds", rounds.value);
}
</script>

<style>
h1 {
  font-size: 4rem;
}

#menu {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  width: 25%;
}
button {
  border: none;
  background: #0faf87;
  color: #fff;
  font-weight: 500;
  border-radius: 6px;
  text-align: center;
  font-size: 1.75rem;
  letter-spacing: 0.05rem;
  padding: 0.5rem 4rem;
  cursor: pointer;
  margin-right: 2rem;
}

#menu > span {
  font-size: 1.25rem;
}

#rounds {
  outline: none;
  border: none;
  color: #2c3e50;
  border-radius: 6px;
  font-size: 1.5rem;
  padding: 0.25rem 0.5rem;
}
</style>
