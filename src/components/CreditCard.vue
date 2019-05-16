<template>
    <article class="card">
        <div class="d-flex">
            <div>
                <h1>{{ card.offer_name }}</h1>
                <div v-if="card.bottom_line">
                    <h3>Our Bottom Line</h3> 
                    {{ card.bottom_line }} <!-- also need to eliminate empty <p></p> tags and set to v-html -->
                </div>
                <a v-if="card.review_url" :href="card.review_url">Read Full Review</a>
                <div v-if="card.marketing_bullets">
                    <h3>Highlights</h3>
                    <p v-html="card.marketing_bullets"></p>
                </div>
                <h3>Fees</h3>
                <p>Annual Fee: {{ card.annual_fee }}</p>
                <p v-if="card.balance_transfer_fee">Balance Transfer Fee: {{ card.balance_transfer_fee }}</p>
                <h3>APRs</h3>
                <p>Regular APR: {{ card.regular_apr }}</p>
                <p>Intro Purchase APR: {{ card.intro_purchase_apr }}</p> <!-- check for "N/A" and possibly filter out -->
                <p>Intro Transfer APR: {{ card.intro_transfer_apr }}</p> <!-- check for "N/A" and possibly filter out -->
            </div>
            <div>
                <img :src="card.offer_image" :alt="card.offer_name">
                <div class="d-flex">
                    <p>APRS Rating: {{ card.aprs_rating }} / 5</p>
                    <p>Fees Rating: {{ card.fees_rating }} / 5</p>
                    <p>Overall Rating: {{ card.star_rating }} / 5</p>
                </div>
                <div v-if="card.what_we_like">
                    <h3>What We Like</h3>
                    <div v-html="card.what_we_like"></div>
                </div>
                <div>
                    <p v-if="card.bonus">Bonus: {{ card.bonus }}</p>
                    Rewards: <p v-if="card.rewards_program">{{ card.rewards_program }}</p> <!-- check for "N/A" and possibly filter out -->
                </div>
            </div>
        </div>
        <a v-if="card.affiliate_link" :href="card.affiliate_link">Apply Now</a>
        <br><a v-if="card.terms_and_conditions_link" :href="card.terms_and_conditions_link">Terms and Conditions</a>
    </article>
</template>

<script>
export default {
    name: "CreditCard",
    props: {
        card: Object,
    }
}
</script>

<style>

</style>
