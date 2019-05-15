<template>
    <div class="card">
        <h3>{{ card_type }} ({{ credit_rating }})</h3>
        <img v-if="card1" :src="card1.offer_image" alt="">
    </div>
</template>

<script>
    export default {
		name: "CreditCard",
		props: {
            card1: Object,
            card_type: String,
            credit_rating: String
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