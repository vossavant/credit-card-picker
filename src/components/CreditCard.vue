<template>
    <div>
        <h3>Type: {{ card_type }} // Credit: {{ credit_rating }}</h3>
        <p v-if="intro_text">{{ intro_text }}</p>
        <p v-if="cta_text" v-html="cta_text"></p>
        <p v-if="error_text" v-html="error_text"></p>

        <!-- this article will eventually be another component -->
        <article class="card" v-if="card1">
            <div class="d-flex">
                <div>
                    <h1>{{ card1.offer_name }}</h1>
                    <div v-if="card1.bottom_line">
                        <h3>Our Bottom Line</h3> 
                        {{ card1.bottom_line }} <!-- also need to eliminate empty <p></p> tags and set to v-html -->
                    </div>
                    <a v-if="card1.review_url" :href="card1.review_url">Read Full Review</a>
                    <div v-if="card1.marketing_bullets">
                        <h3>Highlights</h3>
                        <p v-html="card1.marketing_bullets"></p>
                    </div>
                    <h3>Fees</h3>
                    <p>Annual Fee: {{ card1.annual_fee }}</p>
                    <p v-if="card1.balance_transfer_fee">Balance Transfer Fee: {{ card1.balance_transfer_fee }}</p>
                    <h3>APRs</h3>
                    <p>Regular APR: {{ card1.regular_apr }}</p>
                    <p>Intro Purchase APR: {{ card1.intro_purchase_apr }}</p> <!-- check for "N/A" and possibly filter out -->
                    <p>Intro Transfer APR: {{ card1.intro_transfer_apr }}</p> <!-- check for "N/A" and possibly filter out -->
                </div>
                <div>
                    <img :src="card1.offer_image" :alt="card1.offer_name">
                    <div class="d-flex">
                        <p>APRS Rating: {{ card1.aprs_rating }} / 5</p>
                        <p>Fees Rating: {{ card1.fees_rating }} / 5</p>
                        <p>Overall Rating: {{ card1.star_rating }} / 5</p>
                    </div>
                    <div v-if="card1.what_we_like">
                        <h3>What We Like</h3>
                        <div v-html="card1.what_we_like"></div>
                    </div>
                    <div>
                        <p v-if="card1.bonus">Bonus: {{ card1.bonus }}</p>
                        Rewards: <p v-if="card1.rewards_program">{{ card1.rewards_program }}</p> <!-- check for "N/A" and possibly filter out -->
                    </div>
                </div>
            </div>
            <a v-if="card1.affiliate_link" :href="card1.affiliate_link">Apply Now</a>
            <br><a v-if="card1.terms_and_conditions_link" :href="card1.terms_and_conditions_link">Terms and Conditions</a>
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

<style lang="scss" scoped>
    // TODO: this class needn't be scoped
    .d-flex {
        display: flex;
    }

    .card {
        border: 1px solid #ccc;
        padding: 40px;
        
        &__name {
            
        }
    }
</style>