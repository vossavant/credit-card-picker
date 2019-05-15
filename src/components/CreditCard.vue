<template>
    <div>
        <h3>{{ card_type }}</h3>
    </div>
</template>

<script>
    export default {
		name: "CreditCard",
		props: {
			card_type: String
		}
	};
</script>

<style scoped>
    h3 {
        color: palevioletred;
    }
</style>