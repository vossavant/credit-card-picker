<template>
	<div class="home">
		<HelloWorld msg="Welcome to Your Vue.js App"/>
		<pre>{{ status }}</pre>
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
			this.loadJSON();
		},
		data() {
			return {
				status: ""
			};
		},
		methods: {
			loadJSON() {
				this.status = "Loading JSON...";
				let self = this;
				axios
					.get(
						// "https://jsonplaceholder.typicode.com/posts/2"
						'http://localhost:8080/credit-cards.json'
					)
					.then(function(response) {
						self.status = response.data;
					})
					.catch(function(error) {
						self.status = "An error occurred: " + error;
					});
			}
		}
	};
</script>
