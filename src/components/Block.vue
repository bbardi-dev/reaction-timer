<template>
  <div v-if="showBlock" id="block" @click="stopTimer">Click me!</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Block",
  props: ["delay"],
  data() {
    return {
      showBlock: false,
      timer: 0,
      reactionTime: 0,
    };
  },
  mounted() {
    setTimeout(() => {
      this.showBlock = true;
      this.startTimer();
    }, this.delay);
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => {
        this.reactionTime += 10;
      }, 10);
    },
    stopTimer() {
      clearInterval(this.timer);
      this.showBlock = false;
    },
  },
});
</script>

<style>
#block {
  width: 320px;
  border-radius: 24px;
  background: #0faf87;
  color: #fff;
  text-align: center;
  padding: 6rem 0;
  margin: 5rem auto;
  font-size: 3rem;
  font-weight: 600;
  cursor: pointer;
}
</style>
