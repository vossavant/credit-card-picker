<template>
	<a :href="link">{{ text }}</a>
</template>

<script>
	export default {
		props: {
			link: {
				type: String,
				required: true,
				default: "#"
			},
			text: {
				type: String,
				required: true,
				default: "Click Me"
			}
		}
	};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";
	@import "../scss/mixins.scss";

	a {
		background: $ascent_secondary_cta;
		border-radius: $ascent_border_radius;
		color: white;
		display: inline-block;
		font-size: 1rem;
		font-weight: 700;
		line-height: 3rem;
		margin-top: 2rem;
		padding: 0 3rem;
        transition: 
            background 250ms ease-in-out, 
            box-shadow 250ms ease-in-out,
			transform 250ms ease-in-out;

		@include max-device("phone-landscape") {
			line-height: 4rem;
			margin-top: 1rem;
			text-align: center;
			width: 100%;
		}

		&:hover {
			background: darken($ascent_secondary_cta, 5%);
			box-shadow: 0 0.25rem 0.5rem transparentize(black, 0.8);
			transform: translate3d(-2px, -2px, 0);
			text-decoration: none;
		}
	}
</style>
