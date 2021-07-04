<template>
	<select v-model="selected">
		<option value="0">Select country</option>
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