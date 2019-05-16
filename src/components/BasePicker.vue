<template>
	<div class="picker" v-if="options.length">
		<img v-if="icon" :src="icon" alt="">
		<label>{{ label }}
			<select v-model="selectedOption" @change="$emit('optionSelected', $event.target.value)">
				<option disabled value>Choose an option...</option>
				<option
					v-for="(option, index) in options"
					:value="option"
					:key="index"
				>{{ addSpacesAndCapitalize(option) }}</option>
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
			icon: {
				required: false,
				type: String
			},
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
			addSpacesAndCapitalize(option) {
				return option
					.replace("_", " ")
					.replace(/\b\w/g, l => l.toUpperCase());
			}
		}
	};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";

	.picker {
		background: $ascent_primary;
		border-radius: $ascent_border_radius;
		box-shadow: 0 18px 20px transparentize(black, 0.8);
		color: white;
		flex-grow: 1;
		margin: 0 1rem;
		padding: 2rem;
		text-align: center;
	}
	
	label {
		display: block;
		font: $ascent_heading_h3;
	}

	select {
		border-color: $ascent_primary_heading;
		font-size: 1rem;
		height: 2rem;
		margin: 1rem 0 0;
		width: 100%;
	}
</style>