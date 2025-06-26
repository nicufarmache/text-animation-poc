<script setup>
import Hero from './components/Hero.vue'
import Animated from './components/Animated.vue'
import Staggered from './components/Staggered.vue'
</script>





<template>

  <Hero>
    This is an example text with an <Animated>animated</Animated> word.
  </Hero>

  <Hero>
    This is another example text with <Staggered>staggered</Staggered> animation.
  </Hero>

  <Hero>
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
