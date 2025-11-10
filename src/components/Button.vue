<script setup>
</script>

<template>
	<button class="button">
		<div>
			<slot name="icon" />
			<slot name="text" />
		</div>
	</button>
</template>

<style scoped>
	.button {
		padding: 14px;

		color: var(--color-primary);
		font-family: var(--font);
		font-size: 20px;
		font-weight: 600;

		border: none;
		border-radius: 10px;
		cursor: pointer;
		background: var(--gradient);
	}

	.button:hover {
		background: var(--gradient-inverted);
	}
</style>
