<script setup>
import Button from './components/Button.vue'
</script>

<template>
	<main class="main">
		<Button>
			<template #icon> + </template>
			<template #text>Сохранить</template>
		</Button>
	</main>
</template>

<style scoped>
	.main {
		padding: 60px 50px;

		background-color: var(--color-bg-main);
		border-radius: 25px;
	}
</style>
