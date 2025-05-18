<script setup>
import { ref, computed } from 'vue';
import FlowerLeaf from './FlowerLeaf.vue';

const { options = [] } = defineProps({
  options: {
    type: Array,
    default: []
  }
})

const ColorMap = [
  ['#4E65FF', '#92EFFD'],
  ['#BFF098', '#6FD6FF'],
  ['#FF61D2', '#FE9090'],
  ['#D8B5FF', '#1EAE98'],
  ['#EA8D8D', '#A890FE'],
  ['#FF5F6D', '#FFC371'],
]

const width = 200
const pad = 10
const degGap = 4
const circleWidth = ref(30)
const selectGap = ref(10)

function getDeg(width, pad) {
  const l = Math.sqrt(Math.pow(width * 3 / 4 - 0, 2) + Math.pow(pad - width / 6, 2))
  const m = width / 6 - pad
  const sinValue = m / l
  const deg = Math.asin(sinValue) * 180 / Math.PI
  return deg
}

const computedOptions = computed(() => {
  const isEven = options.length % 2 === 0
  const deg = getDeg(width, pad)
  const singleDeg = deg + degGap

  let order = Math.floor(options.length / 2)
  const startDeg = isEven
    ? (order - 0.5) * singleDeg
    : order * singleDeg

  return options.map((option, index) => {
    const endDeg = isEven
      ? -(order-- - 0.5) * singleDeg
      : -(order--) * singleDeg
    return {
      ...option,
      delay: index * 1,
      startDeg,
      endDeg
    }
  })
})

console.log('computedOptions', computedOptions.value)
</script>


<template>

  <div class="flower-select"
       :style="{ width: `${circleWidth}px`, height: `${circleWidth}px`, '--top': `${-(width / 6 - circleWidth / 2)}px` }">
    <FlowerLeaf v-for="(option, index) in computedOptions"
                :key="option.value"
                :width
                :pad
                :startDeg="option.startDeg"
                :endDeg="option.endDeg"
                :circleWidth
                :selectGap
                :stopColor="ColorMap[index % ColorMap.length]"
                :delay="option.delay" />
  </div>
</template>

<style scoped
       lang="less">
      .flower-select {
        position: relative;
        background-color: red;
        border-radius: 50%;
        z-index: 1;

        >div {
          left: 50%;
          top: var(--top);
        }
      }
    </style>
