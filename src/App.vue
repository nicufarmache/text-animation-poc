<script setup>
import { ref } from 'vue'
import Hero from './components/Hero.vue'
import Animated from './components/Animated.vue'
import Staggered from './components/Staggered.vue'


const page = ref(0);

</script>





<template>

  <navigation>
    <button @click="page = 0">Simple</button>
    <button @click="page = 1">Staggered</button>
    <button @click="page = 2">Chinese</button>
    <button @click="page = 3">Arabic</button>
    <button @click="page = 4">With Space</button>
  </navigation>

  <Hero v-if="page === 0">
    This is an example text with an <Animated>animated</Animated> word.
  </Hero>

  <Hero v-if="page === 1">
    This is another example text with <Staggered>staggered</Staggered> animation.
  </Hero>

  <Hero v-if="page === 2">
    这是带有动<Staggered>画单词的中文</Staggered>示例文本
  </Hero>

  <Hero v-if="page === 3">
    هذا نص نموذجي<Staggered> باللغة العربية</Staggered> مع كلمة متحركة
  </Hero>

  <Hero v-if="page === 4">
    Example <Staggered>with&nbsp;space</Staggered>.
  </Hero>

</template>





<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
