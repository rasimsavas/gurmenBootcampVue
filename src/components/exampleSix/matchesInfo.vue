<template>
    <div class="competition-item">
        <div class="info--container">
            <span class="font-weight-bold">{{match}}</span>
            <small class="text-muted mt-5"><i>{{matchTime}}</i></small>
        </div>
        <div class="rates">
            <matchRate v-for="rate in rates" :rate="rate" :key="{rate}" @select-rate="selectRate"></matchRate>
        </div>
    </div>
</template>

<script>
import matchRate from './matchRate.vue';

export default {
    methods: {
        selectRate(rate) {
            this.$emit('selected-rate-with-match', this.match, this.matchTime, rate);
        },
    },
    props: {
        match: String,
        matchTime: String,
        rates: Array
    },
    components: {
        matchRate
    },
}
</script>
