<template>
	<div>
		<CreditCard v-for="card in creditCards" v-bind="card" />
		<pre>{{ creditCards }}</pre>
	</div>
</template>

<script>
	// @ is an alias to /src
	import CreditCard from "@/components/CreditCard.vue";
	const axios = require('axios');

	export default {
		name: "home",
		components: {
			CreditCard
		},
		created() {
			this.loadCreditCardData();
		},
		data() {
			return {
				creditCards: {}
			};
		},
		methods: {
			loadCreditCardData() {
				let self = this;
				axios
					.get(
						'http://localhost:8080/credit-cards.json'
					)
					.then(function(response) {
						self.creditCards = response.data;
					})
					.catch(function(error) {
						self.creditCards = "Something went wrong while fetching the available credit cards: " + error;
					});
			}
		}
	};
</script>
