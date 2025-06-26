<script setup>
import { ref, computed, provide, watch } from 'vue'
import Hero from './components/Hero.vue'
import Staggered from './components/Staggered.vue'

const durationModel = ref(1200);
const delayModel = ref(300);
const strokeWidthModel = ref(700);

const duration = computed(() => durationModel.value / 1000);
const delay = computed(() => delayModel.value / 1000);
const strokeWidth = computed(() => strokeWidthModel.value / 1000);

provide('duration', duration);
provide('delay', delay);
provide('strokeWidth', strokeWidth);

let timer;
watch([duration, delay, strokeWidth], () => {
  console.log('watch');
  if (timer) clearTimeout(timer);
  timer = setTimeout(() => {
    console.log(duration.value);
    console.log(delay.value);
    console.log(strokeWidth.value);

    const current = page.value;
    page.value = -1;
    setTimeout(() => {
      page.value = current;
    }, 0);
  }, 200);
})

const page = ref(0);

</script>

<template>

  <nav>
    <button @click="page = 0">Simple</button>
    <button @click="page = 1">Chinese</button>
    <button @click="page = 2">Arabic</button>
    <button @click="page = 3">With Space</button>
  </nav>

  <Hero v-if="page === 0">
    This is an example text with an <Staggered>animated</Staggered> word.
  </Hero>

  <Hero v-if="page === 1">
    这是带有动<Staggered>画单词的中文</Staggered>示例文本
  </Hero>

  <Hero v-if="page === 2">
    هذا نص نموذجي<Staggered> باللغة العربية</Staggered> مع كلمة متحركة
  </Hero>

  <Hero v-if="page === 3">
    Example <Staggered>with&nbsp;space</Staggered>.
  </Hero>

  <div class="card">
    <label>
      Duration:
      <input v-model="durationModel" type="range" id="duration" name="volume" min="0" max="5000" />
      <div class="value">{{ durationModel }} ms</div>
    </label>
    <label>
      Delay:
      <input v-model="delayModel" type="range" id="delay" name="volume" min="0" max="500" />
      <div class="value">{{ delayModel }} ms</div>
    </label>
    <label>Stroke Width: <input v-model="strokeWidthModel" type="range" id="stroke" name="volume" min="0" max="1000" />
      <div class="value">{{ strokeWidth }} em</div>
    </label>
  </div>

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
label {
  display: flex;
  gap: 1em;

  @media (max-width: 480px) {
    flex-direction: column;
    align-items: flex-start;
    gap: 0.5em;
  }
}
.value {
  width: 70px;
  text-align: right;

  @media (max-width: 480px) {
    text-align: left;
  }
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}</style>
