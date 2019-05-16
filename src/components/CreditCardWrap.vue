<template>
    <div>
        <h3>Type: {{ card_type }} // Credit: {{ credit_rating }}</h3>
        <p v-if="intro_text">{{ intro_text }}</p>
        <p v-if="cta_text" v-html="cta_text"></p>
        <p v-if="error_text" v-html="error_text"></p>

        <CreditCard v-bind:card="card1" v-if="card1" />
        <CreditCard v-bind:card="card2" v-if="card2" />
    </div>
</template>

<script>
    import CreditCard from "@/components/CreditCard.vue";
    export default {
        components: {
			CreditCard
		},
		name: "CreditCardWrap",
		props: {
            card1: Object,
            card2: Object,
            card_type: String,
            credit_rating: String,
            cta_text: String,
            error_text: String,
            intro_text: String
        }
	};
</script>

<style lang="scss" scoped>
    .card {
        border: 1px solid #ccc;
        padding: 40px;
        
        &__name {
            
        }
    }
</style>