<script setup>
import Stat from './components/Stat.vue'
import CitySelect from './components/CitySelect.vue'
import { computed, ref } from 'vue'
import Error from './components/Error.vue'
import DayCard from './components/DayCard.vue'

const API_ENDPOINT = 'https://api.weatherapi.com/v1'

const errorMap = new Map([[1006, 'Указанный город не найден']])

const data = ref()
const error = ref()

const errorDisplay = computed(() => {
	return errorMap.get(error?.value?.error?.code)
})

const dataModified = computed(() => {
	return [
		{
			label: 'Влажность',
			stat: data.value?.current?.humidity + ' %'
		},
		{
			label: 'Облачность',
			stat: data.value?.current?.cloud + ' %'
		},
		{
			label: 'Ветер',
			stat: data.value?.current?.wind_kph + ' км/ч'
		}
	]
})

async function getCity(city) {
	const params = new URLSearchParams({
		q: city,
		lang: 'ru',
		key: '878b492923b34390a9e153047251211',
		days: 4
	})

	const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`)

	if (res.status !== 200) {
		error.value = await res.json()
		data.value = null
		return
	}

	error.value = null
	data.value = await res.json()
}
</script>

<template>
	<main class="main">
		<Error :error="errorDisplay" />
		<div class="stat-data">
			<div class="stat-list">
				<Stat v-for="item in dataModified" :key="item.label" v-bind="item" />
			</div>
			<div v-if="data" class="day-card-list">
				<DayCard
					v-for="item in data?.forecast?.forecastday"
					:key="item.date"
					:date="new Date(item.date)"
					:temp="item.day.avgtemp_c"
					:weather-code="item.day.condition.code"
				/>
			</div>
		</div>
		<CitySelect @select-city="getCity" />
	</main>
</template>

<style scoped>
.main {
	padding: 60px 50px;

	background-color: var(--color-bg-main);
	border-radius: 25px;
}

.day-card-list {
	display: flex;
	gap: 1px;
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
