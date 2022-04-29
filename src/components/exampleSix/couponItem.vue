<template>
    <div class="coupon-item">
        <div class="w-100 mb-5 d-flex justify-content-between align-items-center">
            <span class="font-weight-bold">{{match}}</span>
            <span class="font-weight-bold text-info">{{rate}}</span>
        </div>
        
        <div class="w-100 d-flex justify-content-between align-items-center">
            <small class="mt-5">Maç Sonucu : <span class="font-weight-bold">{{rateIndex}}</span></small>
            <small class="text-muted">{{matchTime}}</small>
        </div>
        <div class="css--palette text-center">
            <button class="btn-sm btn-danger" @click="deleteMatch"><span class="font-weight-bold">X</span></button>
        </div>
    </div>
</template>

<script>

export default {
    inject: ['bets'],
    props: {
        match: String,
        matchTime: String,
        rate: Number,
        rateIndex: Number,
    },
    methods: {
        deleteMatch() {
            let tmp = this.bets.findIndex(b => b.match === this.match && b.matchTime === this.matchTime);
            this.bets.splice(tmp, 1);
            this.$parent.calculateTotalRate();
        }
    }
}
</script>

<style scoped>
.div button{
    padding: 5px;
}
</style>