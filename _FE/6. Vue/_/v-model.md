```vue
<template>
	<input type='text' v-model="userName" />
	<input type='password' v-model="userPass" />
	<input type='email' v-model="userEmail" />
	<p>{{ userName }}</p>
	<p>{{ userPass }}</p>
	<p>{{ userEmail }}</p>
</template>

<script setup>
	const userName = ref('');
	const userPass = ref('');
	const userEmail = ref('');
</script>

<style scoped>Здесь стили</style>
```

Привязывает значение инпута (практически любого) к реактивной переменной

