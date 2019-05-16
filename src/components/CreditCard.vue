<template>
    <div class="card">
        <h3>Type: {{ card_type }} // Credit: {{ credit_rating }}</h3>
        <p v-if="intro_text">{{ intro_text }}</p>
        <p v-if="cta_text" v-html="cta_text"></p>
        <p v-if="error_text" v-html="error_text"></p>

        <!-- this article will eventually be another component -->
        <article v-if="card1">
            <img :src="card1.offer_image" :alt="card1.offer_name">
            <h1>{{ card1.offer_name }}</h1>
            <a v-if="card1.review_url" :href="card1.review_url">Our Review</a>
            <div v-html="card1.what_we_like"></div>
            <p>Annual Fee: {{ card1.annual_fee }}</p>
            <p>Star Rating: {{ card1.star_rating }} / 5</p>
            <p>APRS Rating: {{ card1.aprs_rating }} / 5</p>
            <p>Fees Rating: {{ card1.fees_rating }} / 5</p>
            <p v-if="card1.balance_transfer_fee">Balance Transfer Fee: {{ card1.balance_transfer_fee }}</p>
            <p v-if="card1.bonus">Bonus: {{ card1.bonus }}</p>
            <p v-if="card1.bottom_line">Our Bottom Line: {{ card1.bottom_line }}</p> <!-- also need to eliminate empty <p></p> tags and set to v-html -->
            <p>Intro Purchase APR: {{ card1.intro_purchase_apr }}</p> <!-- check for "N/A" and possibly filter out -->
            <p>Intro Transfer APR: {{ card1.intro_transfer_apr }}</p> <!-- check for "N/A" and possibly filter out -->
            <p>Regular APR: {{ card1.regular_apr }}</p>
            <p v-if="card1.rewards_program">{{ card1.rewards_program }}</p> <!-- check for "N/A" and possibly filter out -->
            <p><strong>Highlights:</strong></p>
            <p v-html="card1.marketing_bullets"></p>
            <a v-if="card1.affiliate_link" :href="card1.affiliate_link">Apply Now</a>
            <a v-if="card1.terms_and_conditions_link" :href="card1.terms_and_conditions_link">Terms and Conditions</a>
        </article>

        <!-- don't forget card2 -->
    </div>
</template>

<script>
    export default {
		name: "CreditCard",
		props: {
            card1: Object,
            card_type: String,
            credit_rating: String,
            cta_text: String,
            error_text: String,
            intro_text: String
        }
	};
</script>

<style scoped>
    h3 {
        color: palevioletred;
    }

    .card {
        border: 2px solid gray;
        padding: 20px;
        margin-bottom: 20px;
    }
</style>