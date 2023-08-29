<template>
  <p>Reaction time: {{ score }} ms</p>
  <p> {{ rank }}</p>
</template>

<script setup>
import { onMounted, ref } from "vue";

const props = defineProps({
  score: {
    type: Number,
  },
});

const rank = ref(null);

onMounted(() => {
  switch (true) {
    case props.score < 250:
      rank.value = "fast enough";
      break;
    case props.score > 250 && props.score < 400:
      rank.value = "not bad";
      break;
    default:
      rank.value = "you're a piece of sh*t";
  }
});
</script>

<style lang="scss" scoped></style>
