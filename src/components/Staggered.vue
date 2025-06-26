<script setup>
import { ref, onMounted } from 'vue'
import Animated from './Animated.vue'

const DELAY = 0.3;
const DURATION = 1.2;
const content = ref('content');
const letters = ref([]);

onMounted(() => {
  const text = content.value.innerText;
  content.value.style.display = 'none';
  letters.value = text.split('');
})
</script>

<template>
  <span class="staggered">
    <span ref="content">
      <slot></slot>
    </span>
    <Animated v-for="(letter, index) in letters" :key="index" :delay="index * DELAY" :duration="DURATION">{{ letter }}</Animated>
  </span>
</template>

<style scoped>
.staggered {
  white-space: nowrap;
}
</style>