<!--
	Credit Card

	Everything you ever wanted to know about a particular
	credit card offer is here :)
-->
<template>
	<article class="cc-offer">
		<div class="d-flex stack-on-tablet">
			<div class="cc-offer__details">
				<header>
					<h1>{{ card.offer_name }}</h1>
					<div>
						<img class="show-on-tablet" :src="card.offer_image" :alt="card.offer_name">
					</div>
				</header>
				
				<div v-if="card.bottom_line && card.bottom_line !== '<p></p>'">
					<h3>Our Bottom Line</h3>
					<div v-html="card.bottom_line"></div>
				</div>
				
				<a v-if="card.review_url" :href="card.review_url">Read our review of this card &raquo;</a>
				
				<BaseButton
					class="show-on-portrait"
					v-if="card.affiliate_link"
					:link="card.affiliate_link"
					text="Apply Now »"
				/>
				
				<div v-if="card.marketing_bullets">
					<h3 class="has-icon has-icon--trophy">Highlights</h3>
					<div v-html="card.marketing_bullets"></div>
				</div>
				
				<div>
					<h3 class="has-icon has-icon--money">Fees</h3>
					<div class="d-flex stack-on-landscape">
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
					<h3 class="has-icon has-icon--hand">APRs</h3>
					<div class="d-flex stack-on-landscape">
						<div class="cc-offer__callout cc-offer__callout--third">
							<h5>Regular APR:</h5>
							<p>{{ card.regular_apr }}</p>
						</div>
						<div class="cc-offer__callout cc-offer__callout--third">
							<h5>Intro Purchase APR:</h5>
							<p>{{ card.intro_purchase_apr }}</p>
						</div>
						<div class="cc-offer__callout cc-offer__callout--third">
							<h5>Intro Transfer APR:</h5>
							<p>{{ card.intro_transfer_apr }}</p>
						</div>
					</div>
				</div>
				
				<BaseButton v-if="card.affiliate_link" :link="card.affiliate_link" text="Apply Now »"/>
				
				<a
					class="cc-offer__terms-link"
					v-if="card.terms_and_conditions_link"
					:href="card.terms_and_conditions_link"
				>Terms and Conditions</a>
			</div>
			
			<aside class="cc-offer__supplemental">
				<img :src="card.offer_image" :alt="card.offer_name">
				<div class="d-flex cc-offer__ratings">
					<div class="cc-offer__rating cc-offer__rating--bold">
						<h5>Overall</h5>
						<div>
							<span>{{ card.star_rating.toFixed(1) }}</span>
							<span>/ 5</span>
						</div>
					</div>
					<div class="cc-offer__rating">
						<h5>APR</h5>
						<div>
							<span>{{ card.aprs_rating.toFixed(1) }}</span>
							<span>/ 5</span>
						</div>
					</div>
					<div class="cc-offer__rating">
						<h5>Fees</h5>
						<div>
							<span>{{ card.fees_rating.toFixed(1) }}</span>
							<span>/ 5</span>
						</div>
					</div>
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
				</div>
			</aside>
		</div>
	</article>
</template>

<script>
	import BaseButton from "@/components/BaseButton.vue";

	export default {
		components: {
			BaseButton
		},

		props: {
			card: Object
		}
	};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";
	@import "../scss/mixins.scss";

	h1 {
		font: $ascent_heading_h2;
		margin-top: 0;

		@include max-device("tablet") {
			font-size: 4.9vw;
			min-width: 66%;
			padding-right: 2rem;
		}

		@include max-device("phone-landscape") {
			font-size: 1.75rem;
		}

		@include max-device("phone-portrait") {
			padding-right: 0;
		}
	}

	h3 {
		border-bottom: 2px solid transparentize($ascent_primary_heading, 0.9);
		padding-bottom: 0.25rem;

		@include max-device("phone-landscape") {
			font-size: 1.25rem;
			line-height: 2rem;
		}

		&.has-icon {
			background: url("../assets/icon-trophy.svg") top right / 32px no-repeat;

			&--hand {
				background-image: url("../assets/icon-hand.svg");
			}

			&--money {
				background-image: url("../assets/icon-money.svg");
			}
		}
	}

	header {
		@include max-device("tablet") {
			display: flex;
		}

		@include max-device("phone-portrait") {
			flex-wrap: wrap;
			justify-content: space-around;
			margin-bottom: 2rem;
		}
	}

	img {
		border-radius: 1rem;
		box-shadow: $ascent_box_shadow;

		@include max-device("tablet") {
			border-radius: 0.5rem;
		}

		@include max-device("phone-portrait") {
			border-radius: 1rem;
		}
	}

	.cc-offer {
		background: white;
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
		box-shadow: $ascent-box-shadow;
		margin: 2rem 0;
		overflow: hidden;

		@include max-device("tablet") {
			box-shadow: $ascent_box_shadow_tablet;
			margin: 1rem 0;
		}

		@include max-device("phone-vintage") {
			box-shadow: none;
			border-radius: 0;
		}

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
		}

		&__callout--half {
			width: 49%;

			@include max-device("phone-landscape") {
				margin-bottom: 0.5rem;
				width: 100%;
			}

			&:last-child {
				margin-bottom: 0;
			}
		}

		&__callout--third {
			width: 32%;

			@include max-device("phone-landscape") {
				margin-bottom: 0.5rem;
				width: 100%;
			}

			&:last-child {
				margin-bottom: 0;
			}
		}

		&__details {
			max-width: 65%;
			padding: 2rem;

			@include max-device("tablet") {
				max-width: none;
			}

			@include max-device("phone-portrait") {
				padding: 1.5rem;
			}

			/deep/ li {
				margin-bottom: 0.5rem;
			}

			/deep/ li:last-child {
				margin-bottom: 0;
			}
		}

		&__details /deep/ ul {
			@include max-device("phone-portrait") {
				padding-left: 2rem;
			}
		}

		&__rating {
			padding: 0.5rem;
			width: 30%;

			@include max-device("tablet") {
				padding: 1rem;
			}

			@include max-device("phone-portrait") {
				padding: 0.5rem;
			}

			div {
				letter-spacing: -0.05em;
				margin: 0;
			}

			h5 {
				margin: 0;
			}

			&--bold {
				background: white;
				border-radius: $ascent_border_radius;
				color: $ascent_tertiary_accent;
			}
		}

		&__rating span:first-child {
			font-size: 2.375rem;

			@include max-device("phone-portrait") {
				font-size: 2rem;
			}
		}

		&__rating span:last-child {
			opacity: 0.5;
			position: relative;
			left: 0.125rem;
		}

		&__ratings {
			margin-top: 1rem;
		}

		&__supplemental {
			background: $ascent_tertiary_accent;
			color: white;
			max-width: 35%;
			padding: 2rem;

			@include max-device("tablet") {
				max-width: none;
				width: 100%;
			}

			@include max-device("phone-portrait") {
				padding: 1.5rem;
			}

			h3 {
				border-bottom: 2px solid transparentize(white, 0.75);
				color: inherit;
			}

			h5 {
				color: inherit;
			}

			img {
				@include max-device("tablet") {
					display: none;
				}
			}

			/deep/ li {
				line-height: 2rem;
				list-style-image: url("../assets/icon-thumb.svg");
			}

			/deep/ ul {
				list-style: none;
				padding-left: 1.5rem;
			}
		}

		&__terms-link {
			margin-left: 2rem;

			@include max-device("phone-landscape") {
				display: block;
				line-height: 2rem;
				margin-left: 0;
				margin-top: 1rem;
				text-align: center;
			}
		}
	}
</style>