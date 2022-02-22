<template>
  <div
    v-if="showBlock"
    id="block"
    :style="[position, height, width]"
    @click="stopTimer"
  >
    👋
  </div>
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
      width: "",
      height: "",
    };
  },
  created() {
    let x = Math.floor(Math.random() * 200);
    let y = Math.floor(Math.random() * 200);
    this.position = `transform: translate(${x}%, ${y}%);`;
    this.height = `height: ${Math.floor(Math.random() * 100)}px`;
    this.width = `width: ${Math.floor(Math.random() * 360)}px`;
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
