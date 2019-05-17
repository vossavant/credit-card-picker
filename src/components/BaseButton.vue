<template>
    <a :href="link" :style="{ marginTop: topSpacing }">{{ text }}</a>
</template>

<script>
export default {
    props: {
        link: {
            type: String,
            required: true,
            default: '#'
        },
        text: {
            type: String,
            required: true,
            default: 'Click Me'
        },
        topSpacing: {
            type: String,
            default: 0
        }
    }
}
</script>

<style lang="scss" scoped>
    @import '../scss/variables.scss';

    a {
        background: $ascent_secondary_cta;
        border-radius: $ascent_border_radius;
        color: white;
        display: inline-block;
        font-size: 1rem;
        font-weight: 700;
        line-height: 3rem;
        padding: 0 3rem;
    }
</style>
