<script setup lang=ts>
import { ref } from 'vue'
const props = defineProps({
    label: {
        type: String
    }
})
const label = ref(props.label)
</script>

<template>
    <button
      p="2"
      font="mono"
      outline="!none"
      hover:bg="gray-400 opacity-20"
    >
      <slot/>
    </button>
</template>