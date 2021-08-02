<template>
	<select
		@change="onChange"
		v-model="selected"
		class="form-select bg-blue-100 my-10 block w-full border-2 border-blue-400 p-3 rounded"
	>
		<option value="0">Select country</option>
		<option v-for="country in countries" :key="country.ID" :value="country.ID">
			{{ country.Country }}
		</option>
	</select>
</template>

<script>
import { ref } from 'vue';

export default {
	name: 'CountrySelect',
	props: ['countries'],
	emits: ['get-country'],
	setup(props, { emit }){
		const selected = ref(0);

		const onChange = () => {
			const country = props.countries
				.find(country => country.ID === selected.value);
	
			emit('get-country', country);
		}

		return {
			selected,
			onChange
		};
	}
}
</script>