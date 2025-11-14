<script setup>
import Button from './Button.vue'
import IconLocation from '../icons/IconLocation.vue'
import { inject, ref } from 'vue'
import Input from './Input.vue'
import { cityProvide } from '../constants.js'

const city = inject(cityProvide)
const inputValue = ref(city.value)

const isEdited = ref(false)

const select = () => {
	isEdited.value = false
	city.value = inputValue.value
}

const edit = () => {
	isEdited.value = true
}
</script>

<template>
	<div class="city-select">
		<div v-if="isEdited" class="cityInput">
			<Input
				v-model="inputValue"
				v-focus
				placeholder="Введите город"
				type="text"
				@keyup.enter="select"
			/>
			<Button @click="select">Сохранить</Button>
		</div>
		<Button v-else @click="edit">
			<IconLocation />
			Изменить город
		</Button>
	</div>
</template>

<style scoped>
.city-select {
	width: 100%;
}

.cityInput {
	display: flex;
	gap: 12px;
}
</style>
