<script setup lang="ts">
import { ref } from 'vue'
import FlowerSelect from './components/FlowerSelect/FlowerSelect.vue'
import type { FlowerSelectOption } from './types/flower'

const options = ref<FlowerSelectOption>({
  width: 200,
  height: 80,
  fontSize: 20,
  gap: 30,
  direction: 'right',
  data: [
    {
      label: '选项1',
      value: '1',
    },
    {
      label: '选项2',
      value: '2',
    },
    {
      label: '选项3',
      value: '3',
    },
    {
      label: '选项4',
      value: '4',
    },
    {
      label: '选项5',
      value: '5',
    },
  ],
})
</script>

<template>
  <div>
    <FlowerSelect :options/>
  </div>
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
