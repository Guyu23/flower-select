<script setup>
import { ref, computed } from 'vue';

const { width, pad, color } = defineProps({
  width: {
    type: Number,
    default: 270
  },
  pad: {
    type: Number,
    default: 10
  },
  color: {
    type: String,
    default: 'lightblue'
  }
})

const height = computed(() => width / 3)

const l = computed(() => {
  const start = [0, width / 6]
  const end = [width * 3 / 4, pad]
  return Math.sqrt(Math.pow(end[0] - start[0], 2) + Math.pow(end[1] - start[1], 2))
})

const m = computed(() => {
  return width / 6 - pad
})

const r = computed(() => {
  return Math.sqrt(Math.sqrt((Math.pow(m.value, 4) + 4 * Math.pow(m.value, 2) * Math.pow(l.value, 2)) / 2))
})

const d = computed(() => {
  return `M 0 ${width / 6} L ${width * 3 / 4} ${pad} L ${width * 3 / 4} ${height.value - pad} Z`
})

console.log(l.value, m.value, r.value)
</script>

<template>
  <div class='flower-leaf'
       :style="{ width: `${width}px`, height: `${height}px` }">
    <svg width="100%"
         height="100%">
      <path :d
            :stroke="color"
            stroke-width="1"
            fill="none" />
    </svg>

  </div>
</template>

<style scoped>
.flower-leaf {
  position: relative;

  svg {
    border: 1px solid red;
  }
}
</style>