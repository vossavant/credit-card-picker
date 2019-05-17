<!--
	Base Picker

	Creates a stylized dropdown with optional icon. Accepts
	an array of options, passing each through a method that
	makes them more readable.
-->
<template>
	<div class="picker" v-if="options.length">
		<img v-if="icon" :src="icon" alt>
		<label>
			{{ label }}
			<select
				v-model="selectedOption"
				@change="$emit('optionSelected', $event.target.value)"
			>
				<option disabled value>Choose an option...</option>
				<option
					v-for="(option, index) in options"
					:value="option"
					:key="index"
				>{{ addSpacesAndCapitalize(option) }}</option>
			</select>
		</label>
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
				type: Array
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
	@import "../scss/mixins.scss";

	.picker {
		background: $ascent_primary;
		border-radius: $ascent_border_radius;
		box-shadow: $ascent_box_shadow;
		color: white;
		flex-grow: 1;
		margin: 0 1rem;
		padding: 2rem;
		text-align: center;

		@include max-device("tablet") {
			box-shadow: $ascent_box_shadow_tablet;
			margin: 0 0.5rem;
		}

		@include max-device("phone-portrait") {
			margin-top: 1rem;
			padding: 1.5rem;
		}

		@include max-device("phone-vintage") {
			border-radius: 0;
			box-shadow: none;
			margin: 0 0 1px;
			text-align: left;
		}
	}

	label {
		display: block;
		font: $ascent_heading_h3;
	}

	select {
		border-color: $ascent_primary_heading;
		font: 1rem $ascent_font_stack;
		height: 2rem;
		margin: 1rem 0 0;
		width: 100%;
	}
</style>