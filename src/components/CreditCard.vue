<template>
	<article class="cc-offer">
		<div class="d-flex">
			<div class="cc-offer__details">
				<h1>{{ card.offer_name }}</h1>
				<div v-if="card.bottom_line && card.bottom_line !== '<p></p>'">
					<h3>Our Bottom Line</h3>
					{{ card.bottom_line }}
				</div>
				<a v-if="card.review_url" :href="card.review_url">Read Full Review</a>
				<div v-if="card.marketing_bullets">
					<h3>Highlights</h3>
					<p v-html="card.marketing_bullets"></p>
				</div>
				<h3>Fees</h3>
				<p>Annual Fee: {{ card.annual_fee }}</p>
				<p v-if="card.balance_transfer_fee">Balance Transfer Fee: {{ card.balance_transfer_fee }}</p>
				<h3>APRs</h3>
				<p>Regular APR: {{ card.regular_apr }}</p>
				<p>Intro Purchase APR: {{ card.intro_purchase_apr }}</p>
				<!-- check for "N/A" and possibly filter out -->
				<p>Intro Transfer APR: {{ card.intro_transfer_apr }}</p>
				<!-- check for "N/A" and possibly filter out -->
				<a v-if="card.affiliate_link" :href="card.affiliate_link">Apply Now</a>
				<a
					v-if="card.terms_and_conditions_link"
					:href="card.terms_and_conditions_link"
				>Terms and Conditions</a>
			</div>
			<aside class="cc-offer__supplemental">
				<img :src="card.offer_image" :alt="card.offer_name">
				<div class="d-flex">
					<p>APR: {{ card.aprs_rating }} / 5</p>
					<p>Fees: {{ card.fees_rating }} / 5</p>
					<p>Overall: {{ card.star_rating }} / 5</p>
				</div>
				<div v-if="card.what_we_like">
					<h3>What We Like</h3>
					<div v-html="card.what_we_like"></div>
				</div>
				<div>
					<p v-if="card.bonus">Bonus: {{ card.bonus }}</p>Rewards:
					<p v-if="card.rewards_program">{{ card.rewards_program }}</p>
					<!-- check for "N/A" and possibly filter out -->
				</div>
			</aside>
		</div>
	</article>
</template>

<script>
	export default {
		name: "CreditCard",
		props: {
			card: Object
		}
	};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";

	.cc-offer {
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
		box-shadow: $ascent-box-shadow;
		margin: 2rem 0;
		overflow: hidden;

		&__details {
			max-width: 65%;
			padding: 2rem;
		}

		&__supplemental {
			background: $ascent_tertiary_accent;
			color: white;
			max-width: 35%;
			padding: 2rem;

			/deep/ li {
				line-height: 2rem;
				list-style-image: url('../assets/icon-thumb.svg');
			}

			/deep/ ul {
				list-style: none;
				padding-left: 1.5rem;
			}
		}
	}

	h1 {
		font: $ascent_heading_h2;
		margin-top: 0;
	}

	h3 {
		color: inherit;
	}

	img {
		border-radius: 1rem;
		box-shadow: $ascent_box_shadow;
	}
</style>
