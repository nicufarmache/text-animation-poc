<script setup>
import { ref, onMounted, inject } from 'vue'
import Animated from './Animated.vue'

const delay = inject('delay');
const duration = inject('duration');
const strokeWidth = inject('strokeWidth');

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
    <Animated v-for="(letter, index) in letters" :key="index" :delay="index * delay" :duration="duration" :stroke-width="strokeWidth">{{ letter }}</Animated>
  </span>
</template>

<style scoped>
.staggered {
  white-space: nowrap;
}
</style>