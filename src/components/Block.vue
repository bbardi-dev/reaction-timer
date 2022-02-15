<template>
  <div id="block">Click me!</div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "Block",
  props: ["delay"],
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
