<template>
	<section class="cc-list-item">
		<header :class="{ matches: card1 }">
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
		},
		// ideally we could use a filter to check for empty <p></p> tags - maybe with more time!
		// would need to accept the `card` object and iterate over each property
		filters: {
			stripEmptyParagraphTags: function(value) {
				return value.replace('<p></p>', '');
			}
		}
	};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";

	header {
		background: white url("../assets/icon-cancel.svg") center left 2rem no-repeat;
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
		box-shadow: $ascent-box-shadow;
		padding: 2rem 2rem 2rem 8rem;

		h4 {
			margin-top: 0;
		}

		/deep/ p:last-child {
			margin-bottom: 0;
		}

		&.matches {
			background-image: url("../assets/icon-cards.svg");
		}
	}
</style>