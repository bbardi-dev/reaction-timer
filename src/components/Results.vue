<template>
  <p v-if="score">Reaction Time: {{ score }}ms</p>
</template>
<script setup lang="ts">
const props = defineProps<{ score: number }>();
</script>
<style lang=""></style>
