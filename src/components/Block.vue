<template>
  <div v-if="showBlock" id="block" :style="position" @click="stopTimer">👋</div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

const props = defineProps<{ delay: number }>();
const emit = defineEmits(["end"]);

const showBlock = ref(false);
const timer = ref(0);
const reactionTime = ref(0);
const position = ref("");

onMounted(() => {
  function adjustX(x: number) {
    if (Math.floor(Math.random() * 10) > 5) {
      return x;
    } else {
      return x * -1;
    }
  }

  let x = randomInt(10, 400);
  let y = randomInt(10, 300);

  position.value = `transform: translate(${adjustX(x)}%, ${y}%);`;

  setTimeout(() => {
    showBlock.value = true;
    startTimer();
  }, props.delay);
});

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

function startTimer() {
  timer.value = setInterval(() => {
    reactionTime.value += 10;
  }, 10);
}
function stopTimer() {
  clearInterval(timer.value);
  showBlock.value = false;
  emit("end", reactionTime);
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
}
</style>
