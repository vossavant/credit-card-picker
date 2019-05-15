<template>
	<div class="home">
		<HelloWorld msg="Welcome to Your Vue.js App"/>
		<ul>
			<li v-for="item in status" :key="item.id">
				<pre>{{ item }}</pre>
			</li>
		</ul>
		<!-- <pre>{{ status }}</pre> -->
	</div>
</template>

<script>
	// @ is an alias to /src
	import HelloWorld from "@/components/HelloWorld.vue";
	const axios = require('axios');

	export default {
		name: "home",
		components: {
			HelloWorld
		},
		created() {
			this.loadCreditCardData();
		},
		data() {
			return {
				status: ""
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
						self.status = response.data;
					})
					.catch(function(error) {
						self.status = "Something went wrong while fetching the available credit cards: " + error;
					});
			}
		}
	};
</script>
