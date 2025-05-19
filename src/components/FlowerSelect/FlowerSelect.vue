<script
  setup
  lang="ts"
>
import { ref, computed } from 'vue';
import FlowerLeaf from './FlowerLeaf.vue';
import type { FlowerSelectOption } from '@/types/flower';

const { options, width = 50, backgroundColor = 'lightgray' } = defineProps<{
  options: FlowerSelectOption;
  width?: number;
  backgroundColor?: string;
}>()

const ColorMap = [
  ['#4E65FF', '#92EFFD'],
  ['#BFF098', '#6FD6FF'],
  ['#FF61D2', '#FE9090'],
  ['#D8B5FF', '#1EAE98'],
  ['#EA8D8D', '#A890FE'],
  ['#FF5F6D', '#FFC371'],
]

const style = computed(() => {
  return {
    width: `${width}px`,
    height: `${width}px`,
    backgroundColor: backgroundColor,
    '--top': `${width / 2 - options.height / 2}px`,
  }
})

const obj = {
  width: 180,
  height: 80,
  delay: 0,
  startAngle: 25,
  endAngle: -25,
  stopColor: ColorMap[1],
  cutWidth: 30,
  fontSize: 20,
  text: '李位力',
}
</script>


<template>

  <div class="flower-select"
       :style>
    <FlowerLeaf v-bind="obj" />
  </div>
</template>

<style
  scoped
  lang="less"
>
.flower-select {
  position: relative;
  border-radius: 50%;
  z-index: 1;

  >div {
    left: 50%;
    top: var(--top);
  }
}
</style>
