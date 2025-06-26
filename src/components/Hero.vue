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
  min-height: calc(100vh - 170px);
  padding-bottom: 1vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 4vh;

  @media (max-width: 768px) {
    font-size: 1.5vh;
    min-height: calc(30vh);
  }
}
</style>
