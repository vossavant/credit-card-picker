<template>
	<section class="cc-list-item">
		<BaseCallout :class="{ noResults: card1 === null }">
			<h4>Here's What We Found...</h4>
			<p v-if="intro_text">{{ intro_text }}</p>
			<div v-if="error_text && error_text !== '<p></p>'" v-html="error_text"></div>
		</BaseCallout>
		<CreditCard :card="card1" v-if="card1"/>
		<CreditCard :card="card2" v-if="card2"/>
		<BaseCallout v-if="cta_text" v-html="cta_text"/>
	</section>
</template>

<script>
	import BaseCallout from "@/components/BaseCallout.vue";
	import CreditCard from "@/components/CreditCard.vue";
	export default {
		components: {
			BaseCallout,
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

	
</style>