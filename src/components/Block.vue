<template>
  <div v-if="showBlock" id="block" :style="position" @click="stopTimer">👋</div>
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
      position: "",
    };
  },
  created() {
    let x = Math.floor(Math.random() * (Math.random() * 500));
    let y = Math.floor(Math.random() * (Math.random() * 500));
    function adjustX(x: number) {
      if (Math.floor(Math.random() * 10) > 5) {
        return x;
      } else {
        return x * -1;
      }
    }
    this.position = `transform: translate(${adjustX(x)}%, ${y}%);`;
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
      this.$emit("end", this.reactionTime);
    },
  },
});
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
