<script setup>
import Button from './Button.vue'
import IconLocation from '../icons/IconLocation.vue'
import { ref } from 'vue'
import Input from './Input.vue'

const emit = defineEmits({
	selectCity: city => city
})

const city = ref('Moscow')
const isEdited = ref(false)

const select = () => {
	isEdited.value = false
	emit('selectCity', city.value)
}

const edit = () => {
	isEdited.value = true
}
</script>

<template>
	<div class="city-select">
		<div v-if="isEdited" class="cityInput">
			<Input v-model="city" type="text" placeholder="Введите город" />
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
	width: 420px;
}

.cityInput {
	display: flex;
	gap: 12px;
}
</style>
