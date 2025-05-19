<script setup>
import { ref } from 'vue'
import FlowerSelect from './components/FlowerSelect/FlowerSelect.vue'

const options = ref<FlowerSelectOption>({
  width: 180,
  height: 80,
  delay: 0,
  startAngle: 25,
  endAngle: -25,
  cutWidth: 30,
  fontSize: 20,
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
