<script setup>
import { ref } from 'vue'
import FlowerSelect from './components/FlowerSelect/FlowerSelect.vue'

const options = ref([
  {
    label: '选项1',
    value: 'option1'
  },
  {
    label: '选项2',
    value: 'option2'
  },
  {
    label: '选项3',
    value: 'option3'
  },
  {
    label: '选项4',
    value: 'option4'
  },
  {
    label: '选项5',
    value: 'option5'
  }
])
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
