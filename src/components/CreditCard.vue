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
				<div>
					<h3>Fees</h3>
					<div class="d-flex">
						<div class="cc-offer__callout cc-offer__callout--half">
							<h5>Annual Fee:</h5>
							<p>{{ card.annual_fee }}</p>
						</div>
						<div v-if="card.balance_transfer_fee" class="cc-offer__callout cc-offer__callout--half">
							<h5>Balance Transfer Fee:</h5>
							<p>{{ card.balance_transfer_fee }}</p>
						</div>
					</div>
				</div>
				<div>
					<h3>APRs</h3>
					<div class="d-flex">
						<div class="cc-offer__callout cc-offer__callout--third">
							<h5>Regular APR:</h5> 
							<p>{{ card.regular_apr }}</p>
						</div>
						<div class="cc-offer__callout cc-offer__callout--third">
							<h5>Intro Purchase APR:</h5> 
							<p>{{ card.intro_purchase_apr }}</p>
							<!-- check for "N/A" and possibly filter out -->
						</div>
						<div class="cc-offer__callout cc-offer__callout--third">
							<h5>Intro Transfer APR:</h5> 
							<p>{{ card.intro_transfer_apr }}</p>
							<!-- check for "N/A" and possibly filter out -->
						</div>
					</div>
				</div>
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
				<div v-if="card.bonus && card.bonus !== 'N/A'">
					<h3>Bonus</h3>
					<p>{{ card.bonus }}</p>
				</div>
				<div v-if="card.rewards_program && card.rewards_program !== 'N/A'">
					<h3>Rewards</h3>
					<p>{{ card.rewards_program }}</p>
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
	
	h1 {
		font: $ascent_heading_h2;
		margin-top: 0;
	}

	h3 {
		border-bottom: 2px solid transparentize($ascent_primary_heading, 0.9);
		padding-bottom: 0.25rem;
	}

	img {
		border-radius: 1rem;
		box-shadow: $ascent_box_shadow;
	}

	.cc-offer {
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
		box-shadow: $ascent-box-shadow;
		margin: 2rem 0;
		overflow: hidden;

		&__callout {
			background: transparentize($ascent_tertiary_accent, 0.95);
			border-radius: $ascent_border-radius;
			padding: 1rem;

			h5 {
				font-weight: 700;
				margin-top: 0;
			}

			p {
				margin: inherit;
			}

			&--half {
				width: 49%;
			}

			&--third {
				width: 32%;
			}
		}
		
		&__details {
			max-width: 65%;
			padding: 2rem;
		}

		&__supplemental {
			background: $ascent_tertiary_accent;
			color: white;
			max-width: 35%;
			padding: 2rem;

			h3 {
				border-bottom: 2px solid transparentize(white, 0.75);
				color: inherit;
			}
			
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
</style>
