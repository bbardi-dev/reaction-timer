<template>
  <div v-if="showBlock" id="block" :style="position" @click="stopTimer">👋</div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

const props = defineProps<{ delay: number }>();
const emit = defineEmits(["end"]);

let startTime: number;
let reactionTime = 0;
const showBlock = ref(false);
const position = ref("");

onMounted(() => {
  let x = adjustCoordinates(randomInt(10, 400));
  let y = adjustCoordinates(randomInt(10, 200));

  position.value = `transform: translate(${x}%, ${y}%);`;

  setTimeout(() => {
    showBlock.value = true;
    startTime = Date.now();
  }, props.delay);
});

function stopTimer() {
  showBlock.value = false;
  reactionTime = Date.now() - startTime;
  emit("end", reactionTime);
}

// Utility functions
function adjustCoordinates(coord: number) {
  if (Math.floor(Math.random() * 10) > 5) {
    return coord;
  } else {
    return coord * -1;
  }
}

function randomInt(min: number, max: number) {
  if (max == null) {
    max = min;
    min = 0;
  }
  if (min > max) {
    let tmp = min;
    min = max;
    max = tmp;
  }
  return Math.floor((max - min + 1) * Math.random() + min);
}
</script>

<style>
#block {
  width: 64px;
  height: 64px;
  border-radius: 24px;
  background: #0faf87;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 3rem;
  margin: 6rem auto;
  cursor: pointer;
  font-size: 2rem;
}
</style>
