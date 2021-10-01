<script setup lang="ts">
import Button from './Button.vue'
import { ref, computed } from 'vue'

const props = defineProps({
  name: { type: String, required: true },
})
const name = props.name
const counter = ref(0)
const doubleCounter = computed(() => counter.value * 2)
const reinitializeCounter = () => counter.value = 0

</script>

<template>
  <h3>{{name}}</h3>
  <div>
    <div flex="~" w="min" border="~ gray-400 opacity-50 rounded-md">
      <Button @click="counter -= 1">-</Button>
      <span m="auto" p="2" border="r l gray-400 opacity-50">{{ counter }}</span>
      <Button @click="counter += 1">+</Button>
    </div>
    <div>Double compteur : {{doubleCounter}}</div>
    <Button @click="reinitializeCounter">Réinitialiser</Button>
  </div>
</template>
