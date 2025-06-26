<script setup>
</script>

<template>
  <div class="hero">
    <h1><slot></slot></h1>
  </div>
</template>

<style scoped>
.hero {
  width: 100%;
  min-height: 100vh;
  padding-bottom: 1vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3vh;
}
</style>
