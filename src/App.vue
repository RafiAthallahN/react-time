<template>
  <div>
    <h1>Halo</h1>
    <button @click="start" :disabled="data.isPlaying">play</button>

    <block v-if="data.isPlaying" :delay="data.delay" @end="endGame" />
    <Result v-if="data.showResult" :score="data.score"/>
  </div>
</template>

<script setup>
import { reactive } from "vue";

import block from "./components/Block.vue";
import Result from "./components/Result.vue";

const data = reactive({
  isPlaying: false,
  delay: null,
  score: null,
  showResult: false,
});

const start = () => {
  data.delay = 2000 + Math.random() * 5000;
  data.isPlaying = !data.isPlaying;
  data.showResult = false
  console.log(data.delay);
  console.log(data.isPlaying);
};

const endGame = (reactionTime) => {
  data.score = reactionTime;
  data.isPlaying = false;
  data.showResult = true
};
</script>

<style lang="scss" scoped></style>
