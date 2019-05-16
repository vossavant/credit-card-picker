<template>
	<div>
		<h1>Credit Card Picker Doohickey</h1>
		<p>We've vetted hundreds of credit cards to bring you the select few leaders in their categories. Check out our top picks by category, some of which are from our partners, to find the best credit card to suit your needs.</p>
		<div class="d-flex">
			<div v-if="creditCardTypes.length">
				<h4>Search by Card Type</h4>
				<select name="" id="">
					<option v-for="type in creditCardTypes" :value="type">
						{{ type }}
					</option>
				</select>
			</div>
			<div v-if="creditCardRatings.length">
				<h4>Search by Credit Rating</h4>
				<select name="" id="">
					<option v-for="rating in creditCardRatings" :value="rating">
						{{ rating }}
					</option>
				</select>
			</div>
		</div>
		<div>
			<pre>{{ creditCards[1] }}</pre>
			
			<CreditCard v-for="card in creditCards" v-bind="card" />
		</div>
	</div>
</template>

<script>
	// @ is an alias to /src
	import CreditCard from "@/components/CreditCard.vue";
	const axios = require("axios");

	export default {
		components: {
			CreditCard
		},
		created() {
			this.loadCreditCardData();
		},
		data() {
			return {
				creditCards: {},
				creditCardRatings: [],
				creditCardTypes: []
			};
		},
		methods: {
			loadCreditCardData() {
				let self = this;
				axios
					.get("http://localhost:8080/credit-cards.json")
					.then(function(response) {
						self.creditCards = response.data;
						// self.creditCardTypes = [...new Set(response.data.map(card => card.card_type))]; // preferred, but doesn't work in IE11
						self.creditCardTypes = response.data
							.map(card => card.card_type)
							.filter(
								(value, index, self) =>
									self.indexOf(value) === index
							);
						self.creditCardRatings = response.data
							.map(card => card.credit_rating)
							.filter(
								(value, index, self) =>
									self.indexOf(value) === index
							);
					})
					.catch(function(error) {
						self.creditCards =
							"Something went wrong while fetching the available credit cards: " +
							error;
					});
			}
		}
	};
</script>

<style lang="scss">
	@import 'scss/base.scss';
</style>
