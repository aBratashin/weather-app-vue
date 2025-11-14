<script setup>
import IconSun from '../icons/weather/IconSun.vue'
import IconCloud from '../icons/weather/IconCloud.vue'
import IconRain from '../icons/weather/IconRain.vue'
import { computed } from 'vue'

const { weatherCode, date, temp, isActive } = defineProps({
	weatherCode: Number,
	date: Date,
	temp: Number,
	isActive: Boolean
})

const iconColor = computed(() => {
	return isActive ? 'var(--color-primary-inverted)' : 'var(--color-primary)'
})
</script>

<template>
	<button :class="{ active: isActive }" class="day-card">
		<IconSun v-if="weatherCode <= 1003" :color="iconColor" />
		<IconRain
			v-if="weatherCode >= 1006 && weatherCode <= 1063"
			:color="iconColor"
		/>
		<IconCloud v-if="weatherCode > 1063" :color="iconColor" />
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
	width: 100%;
	padding: 20px 21px;

	color: var(--color-primary);
	font-size: 20px;

	border: none;
	outline: none;
	background-color: var(--color-bg-card);
	border-radius: 10px;
	box-shadow: 1px 2px 4px 0 #222831;
}

.day-card:not(.active):hover {
	background-color: var(--color-bg-hover);
	cursor: pointer;
}

.day-card__temp {
	font-weight: 700;
}

.active {
	color: var(--color-primary-inverted);

	background-color: var(--color-primary);
}
</style>
