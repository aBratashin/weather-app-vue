<script setup>
import IconSun from '../icons/weather/IconSun.vue'
import IconCloud from '../icons/weather/IconCloud.vue'
import IconRain from '../icons/weather/IconRain.vue'

const { weatherCode, date, temp } = defineProps({
	weatherCode: Number,
	date: Date,
	temp: Number
})
</script>

<template>
	<button class="day-card">
		<IconSun v-if="weatherCode === 1000" />
		<IconRain v-else-if="weatherCode === 1009" />
		<IconCloud v-else />
		<div class="day-card__day">
			{{ date.toLocaleDateString('ru-RU', { weekday: 'short' }) }}
		</div>
		<div class="day-card__temp">{{ temp }} °C</div>
	</button>
</template>

<style scoped>
.day-card {
	display: flex;
	flex-direction: column;
	align-items: center;
	gap: 15px;
	padding: 20px 24px;

	color: var(--color-primary);
	font-size: 20px;

	border: none;
	outline: none;
	background-color: var(--color-bg-card);
	border-radius: 10px;
	box-shadow: 1px 2px 4px 0 #222831;
}

.day-card:hover {
	background-color: var(--color-bg-hover);
	cursor: pointer;
}

.day-card__temp {
	font-weight: 700;
}
</style>
