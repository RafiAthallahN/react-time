<!-- Block.vue -->
<template>
  <div class="block" v-if="showBlock" @click="stopTimer">click me</div>
</template>

<script setup>
import { onMounted, ref, defineProps, onUpdated, onUnmounted, reactive } from "vue";

const emit = defineEmits([
  'end'
])

const props = defineProps({
  delay: Number,
});

const showBlock = ref(false);

const time = reactive({
  timer: null,
  reactionTime: 0
})

onMounted(() => {
  console.log("mounted");
  setTimeout(() => {
    showBlock.value = true;
    startTimer()
    // console.log(props.delay);
  }, props.delay);
});

onUpdated(() => {
  console.log("updated");
});

const startTimer = () => {
  time.timer = setInterval(() => {
    time.reactionTime += 10
  }, 10)
};
const stopTimer = () => {
  clearInterval(time.timer)
  console.log(time.reactionTime)
  emit('end', time.reactionTime)
};

// onUnmounted(()=> {
//   console.log('unmount')
// })
</script>

<style scoped>
.block {
  width: 400px;
  border-radius: 20px;
  background: rgb(146, 45, 201);
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>
