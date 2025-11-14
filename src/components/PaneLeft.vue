<script setup>
import { computed, inject } from 'vue'
import IconLocation from '../icons/IconLocation.vue'
import IconRain from '../icons/weather/IconRain.vue'
import IconSun from '../icons/weather/IconSun.vue'
import IconCloud from '../icons/weather/IconCloud.vue'
import { cityProvide } from '../constants.js'

const { dayData } = defineProps({
	dayData: Object
})

const city = inject(cityProvide)

const day = computed(() => {
	return new Date(dayData.date).toLocaleDateString('ru-RU', {
		weekday: 'long'
	})
})

const date = computed(() => {
	return new Date(dayData.date)
		.toLocaleDateString('ru-RU', {
			day: 'numeric',
			month: 'long',
			year: 'numeric'
		})
		.replace(' г.', '')
})

const temp = computed(() => {
	return dayData.day.avgtemp_c
})

const dayText = computed(() => {
	return dayData.day.condition.text
})

const weatherCode = computed(() => {
	return dayData.day.condition.code
})
</script>

<template>
	<div class="paneLeft">
		<div class="top">
			<div class="day">{{ day }}</div>
			<div class="date">{{ date }}</div>
			<div class="city">
				<IconLocation />
				{{ city }}
			</div>
		</div>
		<div class="bottom">
			<div class="weatherIcon">
				<IconSun v-if="weatherCode <= 1003" :size="95" />
				<IconRain
					v-if="weatherCode >= 1006 && weatherCode <= 1063"
					:size="95"
				/>
				<IconCloud v-if="weatherCode > 1063" :size="95" />
			</div>
			<div class="temp">{{ temp }} °C</div>
			<div class="condition">{{ dayText }}</div>
		</div>
	</div>
</template>

<style scoped>
.paneLeft {
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	height: 100%;
	padding: 48px 32px;
}

.day {
	margin-bottom: 16px;

	font-size: 37px;
	font-weight: 700;
	text-transform: capitalize;
}

.date {
	margin-bottom: 10px;

	font-size: 22px;
	font-weight: 500;
}

.city {
	display: flex;
	align-items: center;
	gap: 8px;

	font-size: 20px;
	font-weight: 600;
}

.weatherIcon {
	margin: 25px;
}

.temp {
	margin-bottom: 9px;

	font-size: 50px;
	font-weight: 700;
}

.condition {
	font-size: 30px;
	font-weight: 700;
}
</style>
