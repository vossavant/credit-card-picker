<!--
	The Intro

	Master heading and intro paragraph for the entire app.
-->
<template>
	<header>
		<img src="@/assets/logo@2x.svg" width="220">
		<h1>Credit Card Picker</h1>
		<p
			class="intro-p"
		>At Acme Finance, we take your spending habits seriously. That's why we've vetted oodles of credit cards and presented only the very finest to you in each category, so that — no matter your creditworthiness — you can find something to fit your spending habits.</p>
	</header>
</template>

<script>
	export default {};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";
	@import "../scss/mixins.scss";

	h1 {
		font: $ascent_heading_hero;

		@include max-device("tablet") {
			font-size: 8.25vw;
		}

		@include max-device("phone-landscape") {
			font-size: 3rem;
		}

		@include max-device("phone-vintage") {
			font-size: 2.5rem;
			margin-top: 0.5rem;
		}
	}

	header {
		@include max-device("phone-vintage") {
			margin: 1.5rem 1.5rem 0;
		}
	}
</style>