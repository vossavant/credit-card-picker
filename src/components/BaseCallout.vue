<template>
    <div class="callout">
        <slot></slot>
    </div>
</template>

<script>
    export default {
        
    }
</script>

<style lang="scss" scoped>
    @import "../scss/variables.scss";

	.callout {
		background: white url("../assets/icon-cards.svg") center left 2rem no-repeat;
		border: 1px solid $ascent_element_border;
		border-radius: $ascent_border_radius;
        box-shadow: $ascent-box-shadow;
        margin: 2rem 0;
		padding: 2rem 2rem 2rem 8rem;

		h4 {
			margin-top: 0;
		}

		/deep/ p:last-child {
			margin-bottom: 0;
		}

		&.loading {
			background: url('../assets/loader.svg') center left 2.75rem / 2rem no-repeat;
		}

		&.noResults {
			background-image: url("../assets/icon-cancel.svg");
		}
	}
</style>
