<template>
	<div>
		<h1>Credit Card Picker Doohickey</h1>
		<p>We've vetted hundreds of credit cards to bring you the select few leaders in their categories. Check out our top picks by category, some of which are from our partners, to find the best credit card to suit your needs.</p>
		<div class="d-flex">
			<CreditCardPicker
				@optionSelected="selectedType = $event"
				label="Search by Card Type"
				:options="creditCardTypes"
			/>
			<CreditCardPicker
				@optionSelected="selectedRating = $event"
				label="Search by Credit Rating"
				:options="creditCardRatings"
			/>
		</div>
		<CreditCardList
			v-show="selectedType === card.card_type && selectedRating === card.credit_rating"
			v-for="card in creditCards"
			v-bind="card"
		/>
		<!-- <pre>{{ creditCards[1] }}</pre> -->
		type: {{ selectedType }} - rating: {{ selectedRating }}
	</div>
</template>

<script>
	// @ is an alias to /src
	import CreditCardList from "@/components/CreditCardList.vue";
	import CreditCardPicker from "@/components/CreditCardPicker.vue";
	const axios = require("axios");

	export default {
		components: {
			CreditCardList,
			CreditCardPicker
		},
		created() {
			this.loadCreditCardData();
		},
		data() {
			return {
				creditCards: {},
				creditCardRatings: [],
				creditCardTypes: [],
				selectedRating: "",
				selectedType: ""
			};
		},
		methods: {
			loadCreditCardData() {
				let self = this;
				axios
					.get("http://localhost:8080/credit-cards.json")
					// .get("https://www.fool.com/the-ascent/api/creditcardrecommendations/")
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
	@import "scss/base.scss";
</style>
