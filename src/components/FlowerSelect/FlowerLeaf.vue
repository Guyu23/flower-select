<script setup>
import { ref, computed } from 'vue';

const { width, pad, text, startDeg, endDeg, stopColor, circleWidth, selectGap } = defineProps({
  width: {
    type: Number,
    default: 320
  },
  pad: {
    type: Number,
    default: 10
  },
  text: {
    type: String,
    default: '默认名称'
  },
  startDeg: {
    type: Number,
    default: 0
  },
  endDeg: {
    type: Number,
    default: 60
  },
  stopColor: {
    type: Array,
    default: ['#2E3192', '#1BFFFF']
  },
  delay: {
    type: Number,
    default: 0
  },
  circleWidth: {
    type: Number,
    default: 100
  },
  selectGap: {
    type: Number,
    default: 5
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
  return m.value * l.value / Math.sqrt(Math.pow(l.value, 2) - Math.pow(m.value, 2))
})


const startArc = computed(() => {
  const r = circleWidth / 2 + selectGap  // gap
  const k = (pad - width / 6) / (width * 3 / 4) // 斜率 y2 - y1 / x2 - x1
  const sinθ = m.value / l.value
  const h = sinθ * r
  const y = height.value / 2 - h
  const y2 = height.value / 2 + h
  const x = Math.cos(Math.asin(sinθ)) * r
  const arcString = `M ${x} ${y2} A ${r} ${r} 0 0 0 ${x} ${y}`
  return arcString
})

const d = computed(() => {
  return `${startArc.value} L ${width * 3 / 4} ${pad} A ${r.value} ${r.value} 1 1 1 ${width * 3 / 4} ${height.value - pad} Z`
})

</script>

<template>
  <div class='flower-leaf'
       :style="{ width: `${width}px`, height: `${height}px`, '--endDeg': endDeg + 'deg', '--startDeg': startDeg + 'deg', '--delay': delay + 's' }">
    <svg width="100%"
         height="100%">
      <g>
        <defs>
          <linearGradient id="gradient"
                          x1="0%"
                          y1="0%"
                          x2="100%"
                          y2="0%">
            <stop offset="0%"
                  :stop-color="stopColor[0]" />
            <stop offset="100%"
                  :stop-color="stopColor[1]" />
          </linearGradient>
        </defs>
      </g>
      <path :d
            fill="url(#gradient)" />
      <text :x="width * 3 / 5"
            :y="height / 2"
            font-size="16"
            style="dominant-baseline: middle; text-anchor: middle;"
            fill="white">
        {{ text }}
      </text>
    </svg>

  </div>
</template>

<style scoped>
.flower-leaf {
  position: absolute;
  transform-origin: left;
  animation: flower-leaf-animation 0.5s ease-in-out forwards;
  animation-delay: var(--delay);
}

@keyframes flower-leaf-animation {
  0% {
    opacity: 0;
    transform: rotate(var(--startDeg));
  }

  100% {
    transform: rotate(var(--endDeg));
    opacity: 1;
  }
}
</style>