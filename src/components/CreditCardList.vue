<template>
	<div>
		<h3>Type: {{ card_type }} // Credit: {{ credit_rating }}</h3>
		<h2>Your Results</h2>
		<p v-if="intro_text">{{ intro_text }}</p>
		<p v-if="error_text" v-html="error_text"></p>

		<CreditCard :card="card1" v-if="card1"/>
		<CreditCard :card="card2" v-if="card2"/>
		
		<p v-if="cta_text" v-html="cta_text"></p>
	</div>
</template>

<script>
	import CreditCard from "@/components/CreditCard.vue";
	export default {
		components: {
			CreditCard
		},
		props: {
			card1: Object,
			card2: Object,
			card_type: {
				required: true,
				type: String
			},
			credit_rating: {
				required: true,
				type: String
			},
			cta_text: String,
			error_text: String,
			intro_text: String
		}
	};
</script>

<style lang="scss" scoped>
	.card {
		border: 1px solid #ccc;
		padding: 40px;

		&__name {
		}
	}
</style>