<template>
	<div class="d-flex">
		<div v-if="types.length">
			<h4>Search by Card Type</h4>
			<select v-model="selectedType" v-on:change="$emit('selectCardType', $event.target.value)">
				<option disabled value>Choose a card type...</option>
				<option
					v-for="(type, index) in types"
					v-bind:value="type"
					:key="index"
				>{{ parseSelectOptions(type) }}</option>
			</select>
			<p>Selected: {{ selectedType }}</p>
		</div>
		<div v-if="ratings.length">
			<h4>Search by Credit Rating</h4>
			<select v-model="selectedRating" v-on:change="$emit('selectCreditRating', $event.target.value)">
				<option disabled value>Choose a credit rating...</option>
				<option
					v-for="(rating, index) in ratings"
					v-bind:value="rating"
					:key="index"
				>{{ parseSelectOptions(rating) }}</option>
			</select>
			<p>Selected: {{ selectedRating }}</p>
		</div>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				selectedRating: "",
				selectedType: ""
			};
		},
		name: "CreditCardPickers",
		props: {
			ratings: Array,
			types: Array
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
