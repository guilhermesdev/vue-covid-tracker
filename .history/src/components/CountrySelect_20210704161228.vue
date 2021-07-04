<template>
	<select v-model="selected" class="form-select bg-blue-100 my-10 block w-full border-2 border-blue-400 p-3 rounded">
		<option value="0">Select country</option>
		<option v-for="country in countries" :key="country.ID" :value="country.ID">
			{{ country.Country }}
		</option>
	</select>
</template>

<script>
export default {
	name: 'CountrySelect',
	props: ['countries'],
	data(){
		return {
			selected: 0
		}
	}
}
</script>