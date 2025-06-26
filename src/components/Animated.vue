<script setup>
import { useId, useTemplateRef, onMounted, ref } from 'vue'

const props = defineProps({
  delay: {
    type: Number,
    default: 0
  },
  duration: {
    type: Number,
    default: 4
  },
  strokeWidth: {
    type: Number,
    default: 0.3
  }
})

const id = useId()
const text = useTemplateRef('text')
const svg = useTemplateRef('svg')

const resize = () => {
  const { width, height } = text.value.getBBox();
  svg.value.style.width = `${width}px`;
}

onMounted(() => {
  resize();
  window.addEventListener('resize', resize);
  window.addEventListener('orientationchange', resize);
  document.fonts.ready.then(resize);
})

</script>

<template>
  <svg ref="svg" class="animated"
    :style="{
       '--animated-delay': `${props.delay}s`,
       '--animated-duration': `${props.duration}s`,
       '--stroke-width': `${props.strokeWidth}em`
    }">
    <symbol :id="`text-${id}`"><text class="no-select" ref="text" x="0" y="100%" dy="-.225em">
        <slot></slot>
      </text></symbol>
    <mask :id="`mask-${id}`">
      <rect id="bg" x="0" y="0" width="100%" height="100%" fill="black" />
      <use :xlink:href="`#text-${id}`" fill="white"></use>
    </mask>
    <use :xlink:href="`#text-${id}`" id="outline" :mask="`url(#mask-${id})`"></use>
    <text ref="text" x="0" y="100%" dy="-.2em" fill="transparent">
      <slot></slot>
    </text>
  </svg>
</template>

<style scoped>

.animated {
  --start-color: currentColor;
  --accent-color: #0088ff;
  --stroke-width: 0.3em;
  display: inline-flex;
  width: 380px;
  height: 1lh;
  vertical-align: text-bottom;
}

.no-select {
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
  pointer-events: none;
}

#outline {
  /* fill-opacity: 0; */
  fill: var(--start-color);
  stroke: var(--accent-color);
  stroke-width: 0;
  stroke-dasharray: 1000, 250;
  stroke-dashoffset: -250;
  stroke-linecap: round;
  stroke-linejoin: round;
  paint-order: fill stroke;
  animation-name: outline;
  animation-duration: var(--animated-duration, 1s);
  animation-fill-mode: forwards;
  animation-delay: var(--animated-delay, 0);
}


@keyframes outline {
  from {
    fill: var(--start-color);
    stroke-width: 0;
    stroke-dashoffset: -250;
    animation-timing-function: ease-in;
  }

  15% {
    fill: var(--start-color);
    stroke-width: calc(var(--stroke-width) * 0.3);
    stroke-dashoffset: -230;
    animation-timing-function: linear;
  }

  85% {
    fill: var(--start-color);
    stroke-width: calc(var(--stroke-width) * 0.6);
    stroke-dashoffset: 0;
    animation-timing-function: linear;
  }

  to {
    fill: var(--accent-color);
    stroke-width: calc(var(--stroke-width) * 1);
    stroke-dashoffset: 0;
    animation-timing-function: ease-out;
  }
}
</style>