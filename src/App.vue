<script setup>
import { onMounted, provide, ref, watch } from 'vue'
import PaneRight from './components/PaneRight.vue'
import { API_ENDPOINT, cityProvide } from './constants.js'
import PaneLeft from './components/PaneLeft.vue'

const apiKey = import.meta.env.VITE_WEATHER_API_KEY
const data = ref()
const error = ref()
const activeIndex = ref(0)
const city = ref('Москва')

provide(cityProvide, city)

watch(city, () => {
	getCity(city.value)
})

onMounted(() => {
	getCity(city.value)
})

async function getCity(city) {
	const params = new URLSearchParams({
		q: city,
		lang: 'ru',
		key: apiKey,
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
		<div class="left">
			<PaneLeft
				v-if="data"
				:day-data="data.forecast.forecastday[activeIndex]"
			/>
		</div>
		<div class="right">
			<PaneRight
				:active-index="activeIndex"
				:data="data"
				:error="error"
				@select-index="i => (activeIndex = i)"
			/>
		</div>
	</main>
</template>

<style scoped>
.main {
	display: flex;
	align-items: center;
	justify-content: center;
}

.left {
	width: 500px;
	height: 680px;

	border-radius: 30px;
	background-image: url('/public/bg.png');
	background-repeat: no-repeat;
	background-size: cover;
}

.right {
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	width: 600px;
	height: 623px;
	padding: 60px 50px;

	background-color: var(--color-bg-main);
	border-radius: 0 25px 25px 0;
}
</style>
