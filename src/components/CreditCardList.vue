<template>
	<section class="cc-list-item">
		<!-- <h3>Type: {{ card_type }} // Credit: {{ credit_rating }}</h3> -->
		<header :class="{ noMatches: error_text }">
			<h4>Here's What We Found...</h4>
			<p v-if="intro_text">{{ intro_text }}</p>
			<div v-if="error_text && error_text !== '<p></p>'" v-html="error_text"></div>
		</header>

		<CreditCard :card="card1" v-if="card1"/>
		<CreditCard :card="card2" v-if="card2"/>

		<p v-if="cta_text" v-html="cta_text"></p>
	</section>
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
	@import "../scss/variables.scss";

	header {
		background: url("../assets/icon-trophy.svg") center left 2rem no-repeat;
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
		padding: 2rem 2rem 2rem 8rem;

		h4 {
			margin-top: 0;
		}

		p:last-of-type {
			margin-bottom: 0;
		}

		&.noMatches {
			background-image: url("../assets/icon-cancel.svg");
		}
	}
</style>