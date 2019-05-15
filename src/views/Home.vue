<template>
	<div class="home">
		<HelloWorld msg="Welcome to Your Vue.js App"/>
		<ul>
			<li v-for="card in creditCards">
				<CreditCard v-bind="card" />
			</li>
		</ul>
		<pre>{{ creditCards }}</pre>
	</div>
</template>

<script>
	// @ is an alias to /src
	import CreditCard from "@/components/CreditCard.vue";
	import HelloWorld from "@/components/HelloWorld.vue";
	const axios = require('axios');

	export default {
		name: "home",
		components: {
			CreditCard,
			HelloWorld
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
