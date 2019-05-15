<template>
	<div>
		{{creditCardTypes}}
		<CreditCard v-for="card in creditCards" v-bind="card"/>
		<pre>{{ creditCards }}</pre>
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
						// self.creditCardTypes = [...new Set(response.data.map(card => card.card_type))]; // doesn't work in IE11
						self.creditCardTypes = response.data
							.map(card => card.card_type)
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
