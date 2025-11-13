<script setup>
const props = defineProps({
	error: String
})

</script>

<template>
	<div v-if="props.error" class="error">{{ props.error }}</div>
</template>

<style scoped>
.error {
	margin-top: -60px;
	margin-bottom: 60px;
	padding: 15px;

	font-size: 18px;
	color: var(--color-primary);
	text-align: center;

	background-color: var(--color-bg-card);
	border-radius: 0 0 25px 25px;
}
</style>
