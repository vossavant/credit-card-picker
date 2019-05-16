<template>
	<div class="ascent-cc-app">
		<TheIntro />
		<div class="d-flex">
			<BasePicker
				@optionSelected="selectedType = $event"
				icon="https://g.foolcdn.com/static/affiliates/project/images/icons/credit-card-white.svg"
				label="Search by Card Type"
				:options="creditCardTypes"
			/>
			<BasePicker
				@optionSelected="selectedRating = $event"
				icon="https://g.foolcdn.com/static/affiliates/project/images/icons/cash-white.svg"
				label="Search by Credit Rating"
				:options="creditCardRatings"
			/>
		</div>
		<CreditCardList
			v-show="showCards(card)"
			v-for="(card, index) in creditCards"
			v-bind="card"
		/>
		<!-- <pre>{{ creditCards }}</pre> -->
	</div>
</template>

<script>
	// @ is an alias to /src
	import BasePicker from "@/components/BasePicker.vue";
	import CreditCardList from "@/components/CreditCardList.vue";
	import TheIntro from "@/components/TheIntro.vue";
	const axios = require("axios");

	export default {
		components: {
			BasePicker,
			CreditCardList,
			TheIntro
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
			},

			showCards(card) {
				return this.selectedType === card.card_type && this.selectedRating === card.credit_rating;
			},
		}
	};
</script>

<style lang="scss">
	@import "scss/base.scss";
</style>
