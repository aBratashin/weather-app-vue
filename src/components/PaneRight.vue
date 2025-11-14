<script setup>
import Error from './Error.vue'
import Stat from './Stat.vue'
import DayCard from './DayCard.vue'
import CitySelect from './CitySelect.vue'
import { computed } from 'vue'
import { errorMap } from '../constants.js'

const { error, data, activeIndex } = defineProps({
	error: Object,
	data: Object,
	activeIndex: Number
})

const emit = defineEmits(['select-index'])

const errorDisplay = computed(() => {
	return errorMap.get(error?.error?.code)
})

const statData = computed(() => {
	if (!data) {
		return []
	}

	return [
		{
			label: 'Ветер',
			stat: data.forecast.forecastday[activeIndex].day.maxwind_kph + ' км/ч'
		},
		{
			label: 'Влажность',
			stat: data.forecast.forecastday[activeIndex].day.avghumidity + ' %'
		},
		{
			label: 'Вероятность дождя',
			stat:
				data.forecast.forecastday[activeIndex].day.daily_chance_of_rain + ' %'
		}
	]
})
</script>

<template>
	<Error v-if="error" :error="errorDisplay" />
	<div v-if="data" class="stat-data">
		<div class="stat-list">
			<Stat v-for="item in statData" :key="item.label" v-bind="item" />
		</div>
		<div class="day-card-list">
			<DayCard
				v-for="(item, index) in data?.forecast?.forecastday"
				:key="item.date"
				:date="new Date(item.date)"
				:temp="item.day.avgtemp_c"
				:weather-code="item.day.condition.code"
				:is-active="activeIndex === index"
				@click="() => emit('select-index', index)"
			/>
		</div>
	</div>
	<CitySelect />
</template>

<style scoped>
.day-card-list {
	display: flex;
	gap: 2px;
}

.stat-data {
	display: flex;
	flex-direction: column;
	gap: 70px;
	margin-bottom: 70px;
}

.stat-list {
	display: flex;
	flex-direction: column;
	gap: 16px;
}
</style>
