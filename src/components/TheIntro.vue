<template>
    <header>
        <h1>Credit Card Picker Doohickey</h1>
        <p class="intro-p">We've vetted hundreds of credit cards to bring you the select few leaders in their categories. Check out our top picks by category, some of which are from our partners, to find the best credit card to suit your needs.</p>
    </header>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
    @import '../scss/variables.scss';
    @import '../scss/mixins.scss';

    h1 {
        font: $ascent_heading_hero;

        @include max-device('tablet') {
            font-size: 8.25vw;
        }

        @include max-device('phone-landscape') {
            font-size: 3rem;
        }

        @include max-device('phone-vintage') {
            font-size: 2.5rem;
            margin-top: 0;
        }
    }

    header {
        @include max-device('phone-vintage') {
            margin: 1rem 1rem 0;
        }
    }
</style>