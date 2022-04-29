<template>
    <div class="rate-item">
        <button class="btn-sm" @click="rateClick">{{rate}}</button>
    </div>
</template>

<script>
export default {
    props: {
        rate: Number,
    },
    methods: {
        rateClick() {
            this.$emit('select-rate', this.rate);
        },
    },
}
</script>
