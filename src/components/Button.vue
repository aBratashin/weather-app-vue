<script setup></script>

<template>
	<button class="button">
		<slot></slot>
	</button>
</template>

<style scoped>
.button {
	display: flex;
	align-items: center;
	justify-content: center;
	gap: 9px;
	height: 53px;
	width: 100%;
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
