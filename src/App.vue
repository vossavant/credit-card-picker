<!--
	App

	Loads app components and immediately fetches credit card info
	so it is ready when the user wants to make a selection.
-->
<template>
	<div class="acme-cc-app">
		<TheIntro />

		<div v-if="creditCards">
			<BaseCallout v-show="!selectedType || !selectedRating">
				<h4>Let's Get Started!</h4>
				<p>To see our top picks, select your preferred <b>card type</b> and a <b>credit rating</b> from below!</p>
			</BaseCallout>

			<BasePickerWrapper>
				<BasePicker
					@optionSelected="selectedType = $event"
					icon="https://g.foolcdn.com/static/affiliates/project/images/icons/credit-card-white.svg"
					label="Search by Card Type"
					:options="creditCardTypes"
				/>
				<BasePicker
					@optionSelected="selectedRating = $event"
					icon="https://g.foolcdn.com/static/affiliates/project/images/icons/goals-white.svg"
					label="Search by Credit Rating"
					:options="creditCardRatings"
				/>
			</BasePickerWrapper>

			<CreditCardList
				v-show="showCards(card)"
				v-for="(card, index) in creditCards"
				v-bind="card"
				:key="index"
			/>
		</div>

		<BaseCallout v-else :class="loadingCalloutClass">
			<div v-if="creditCardError">
				<h4>Oh No!</h4>
				<div v-html="creditCardError"></div>
			</div>
			<div v-else>
				<h4>Reticulating Splines...</h4>
				<p>We're fetching our credit card recommendations from the mother ship. Please hang tight!</p>
			</div>
		</BaseCallout>
	</div>
</template>

<script>
	// @ is an alias to /src
	import BaseCallout from "@/components/BaseCallout.vue";
	import BasePicker from "@/components/BasePicker.vue";
	import BasePickerWrapper from "@/components/BasePickerWrapper.vue";
	import CreditCardList from "@/components/CreditCardList.vue";
	import TheIntro from "@/components/TheIntro.vue";
	const axios = require("axios");

	export default {
		components: {
			BaseCallout,
			BasePicker,
			BasePickerWrapper,
			CreditCardList,
			TheIntro
		},

		created() {
			this.loadCreditCardData();
		},

		data() {
			return {
				creditCards: null,
				creditCardError: null,
				creditCardRatings: [],
				creditCardTypes: [],
				selectedRating: null,
				selectedType: null
			};
		},

		computed: {
			loadingCalloutClass() {
				return {
					loading: this.creditCardError === null,
					noResults: this.creditCardError
				}
			}
		},

		methods: {
			loadCreditCardData() {
				let self = this;
				axios
					// .get("https://www.ryanburney.com/projects/acme-cc-picker/credit-cards.json")
					.get("http://localhost:8081/credit-cards.json")
					.then(function(response) {
						self.creditCards = response.data;
						self.creditCardTypes = [...new Set(response.data.map(card => card.card_type))];
						self.creditCardRatings = [...new Set(response.data.map(card => card.credit_rating))];
						// use the below method if IE11 support is required
						// self.creditCardTypes = response.data
						// 	.map(card => card.card_type)
						// 	.filter(
						// 		(value, index, self) =>
						// 			self.indexOf(value) === index
						// 	);
					})
					.catch(function(error) {
						self.creditCardError =
							"<p>Something went wrong while fetching the available credit cards: <strong>" +
							error + '</strong></p>';
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