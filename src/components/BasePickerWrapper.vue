<!--
	Base Picker Wrapper

	Wraps the BasePicker component in a specially stylized div
    that accounts for negative margins on the pickers.
-->
<template>
	<div class="picker-wrap">
		<slot></slot>
	</div>
</template>

<script>
	export default {};
</script>

<style lang="scss" scoped>
	@import "../scss/variables.scss";
	@import "../scss/mixins.scss";

	.picker-wrap {
		display: flex;
		margin: 2rem -1rem;

		@include max-device("tablet") {
			margin: 1rem -0.5rem;
		}

		@include max-device("phone-portrait") {
			flex-wrap: wrap;
		}

		@include max-device("phone-vintage") {
			margin-left: 0;
			margin-right: 0;
		}
	}
</style>