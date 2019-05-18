<!--
	Base Callout

	Accepts any content in the <slot></slot> below. Helpful for
	presenting important content in a notification-style box.
-->
<template>
	<div class="callout">
		<slot></slot>
	</div>
</template>

<script>
	export default {};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";
	@import "../scss/mixins.scss";

	.callout {
		background: white url("../assets/icon-cards.svg") center left 2rem no-repeat;
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
		box-shadow: $ascent-box-shadow;
		margin: 2rem 0;
		padding: 2rem 2rem 2rem 8rem;
		transition: box-shadow 250ms ease-in-out;

		@include max-device("tablet") {
			box-shadow: $ascent_box_shadow_tablet;
			margin: 1rem 0;
		}

		@include max-device("phone-portrait") {
			background-position: top 1rem center;
			padding: 6rem 1.5rem 1.5rem;
		}

		@include max-device("phone-vintage") {
			border-radius: 0;
			box-shadow: none;
		}

		&:hover {
			box-shadow: $ascent_box_shadow_hover;
		}

		h4 {
			margin-top: 0;
		}

		/deep/ p:last-child {
			margin-bottom: 0;
		}

		&.loading {
			background: url("../assets/loader.svg") center left 2.75rem / 2rem
				no-repeat;
		}

		&.noResults {
			background-image: url("../assets/icon-cancel.svg");
		}
	}
</style>