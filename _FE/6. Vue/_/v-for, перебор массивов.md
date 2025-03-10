```vue
<script setup lang="ts">
import { ref } from 'vue'

const users = ref([
  {name: 'name1', pass: 'pass1'},
  {name: 'name2', pass: 'pass2'},
  {name: 'name3', pass: 'pass3'},
])
</script>

<template>
  <div v-for="(el, idx) in users" :key="idx">
    {{ el.name }} {{ el.pass }}
  </div>
</template>
```