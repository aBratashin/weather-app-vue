<script setup>
import Stat from './components/Stat.vue'
import CitySelect from './components/CitySelect.vue'
import { computed, ref } from 'vue'

let savedCity = ref('Moscow')

let data = ref({
	humidity: 90,
	rain: 0,
	wind: 3
})

const dataModified = computed(() => [
	{
		label: 'Влажность',
		stat: data.value.humidity + '%'
	},
	{
		label: 'Осадки',
		stat: data.value.rain + '%'
	},
	{
		label: 'Ветер',
		stat: data.value.wind + 'м/c'
	}
])

function getCity(city) {
	savedCity.value = city
	data.value.humidity = 20
}
</script>

<template>
	<main class="main">
		<div id="city">{{ savedCity }}</div>
		<Stat
			v-for="item in dataModified"
			:key="item.label"
			v-bind="item"
		/>
		<CitySelect @select-city="getCity" />
	</main>
</template>

<style scoped>
.main {
	padding: 60px 50px;

	background-color: var(--color-bg-main);
	border-radius: 25px;
}
</style>
