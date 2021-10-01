<script>
export default {
    props: {
        name: { type: String, required: true}
    },
    data() {
        return { counter: 0 }
    },
    computed: {
        doubleCounter() { return this.counter * 2 }
    },
    methods: {
        reinitializeCounter() { this.counter = 0 }
    }
}
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
