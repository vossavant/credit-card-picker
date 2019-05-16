<template>
	<div v-if="options.length">
		<label>{{ label }}
			<select v-model="selectedOption" @change="$emit('optionSelected', $event.target.value)">
				<option disabled value>Choose an option...</option>
				<option
					v-for="(option, index) in options"
					:value="option"
					:key="index"
				>{{ parseSelectOptions(option) }}</option>
			</select>
		</label>
		<p>Selected: {{ selectedOption }}</p>
	</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				selectedOption: ""
			};
		},
		props: {
			label: {
				required: true,
				type: String
			},
			options: {
				required: true,
				type: Array,
			}
		},
		methods: {
			parseSelectOptions(option) {
				return option
					.replace("_", " ")
					.replace(/\b\w/g, l => l.toUpperCase());
			}
		}
	};
</script>

<style>
</style>
