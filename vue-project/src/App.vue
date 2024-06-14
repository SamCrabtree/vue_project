<script setup>
import { ref } from 'vue'

const msg = ref('Hello World!')
</script>

<template>
  <pre>
    <h1>Vue Testing Ground</h1>
    <h2>{{ msg }}</h2>
    <input v-model="msg" />
  </pre>
</template>
