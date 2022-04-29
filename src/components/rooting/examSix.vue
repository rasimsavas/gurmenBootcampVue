<template>
<header class="header"> Ek olarak kuponun iceriginden istenilen maclari silmeyi ekledim, bu durumda otomatik olarak kazanc ve oran yeniden hesaplaniyor.</header>
    <div class="container">
      <div class="bet--coupon--app d-flex justify-content-between align-items-start">
        <!-- Mac Listesi-->
        <div class="card competition-list mr-10">
          <div class="card--header">
            <h4>Yakın Zamanda Başlayacak Müsabakalar</h4>
          </div>
          <div class="card--body">
              <matchInfo v-for="match in matches" :key="match" @selected-rate-with-match="selectedRateWithMatch" :match="match.description" :matchTime="match.time" :rates="match.rates"></matchInfo>
          </div>
        </div>
        <!-- Kuponum -->
        <div class="coupon--total--container">
          <div class="card my-coupon">
            <div class="card--header">
              <h4>Kuponum</h4>
            </div>
            <div class="card--body">
              <coupon-item v-for="coupon in bet" :key="coupon" :match="coupon.match" :matchTime="coupon.matchTime" :rate="coupon.rate" :rateIndex="coupon.rateIndex"></coupon-item>
            </div>
          </div>
          <div class="card card-light multiply--container mt-20">
            <h4 class="text-center mb-10">Mislini Seç</h4>
            <div class="multiply--buttons mb-10 d-flex justify-content-center align-items-center" >
                <button v-for="cross in betCross" :key="cross" class="btn btn-outline-info" @click="setCross(cross)">{{cross}}</button>
            </div>
            <div class="coupon--total--container mt-20">
              
              <div class="d-flex justify-content-between align-items-center font-weight-bold">
                <span>Toplam Oran</span>
                <span class="text-info">{{totalRate}}</span>
              </div>
              <div class="d-flex justify-content-between align-items-center mt-5">
                <span>Kupon Tutarı</span>
                <span class="font-weight-bold">{{selectedCross}} TL</span>
              </div>
              <div class="d-flex justify-content-between align-items-center mt-5">
                <span>Tahmini Kazanç</span>
                <span class="font-weight-bold text-info">{{predictedWin}} TL</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import matchInfo from '../exampleSix/matchesInfo.vue';
import couponItem from '../exampleSix/couponItem.vue';

export default {
    data(){
        return {
            matches: [{
                description: 'Beşiktaş x Başakşehir FK',
                time: 'Saat: 22:00',
                rates: [1.50, 2.50, 1.60]
            }, {
                description: 'Fenerbahçe x Galatasaray',
                time: 'Saat: 21:30',
                rates: [4.20, 2.50, 1.30]
            },
            {
                description: 'Trabzonspor x Basaksehir',
                time: 'Saat: 21:00',
                rates: [1.85, 2.50, 2.40]
            },
            {
                description: 'Karagumruk x Hatayspor',
                time: 'Saat: 18:00',
                rates: [2.20, 2.40, 2.30]
            },
            {
                description: 'Eskisehir x Antalya',
                time: 'Saat: 22:30',
                rates: [4.20, 2.40, 1.45]
            },

            ],
            bet: [],
            betCross: [5, 10, 20, 30, 50, 100, 200, 500, 1000, 1500, 2500],
            selectedCross: 0,
            totalRate: 0,
            predictedWin: 0,
            
        }
    },
    provide(){
        return {
            bets: this.bet,
            
        }
    },
    methods: {
        setCross(cross) {
            this.selectedCross = cross;
            this.calculateTotalRate();
        },
        selectedRateWithMatch(match,matchTime, rate){
            const selectedMatch = this.matches.find(m => m.description === match && m.time === matchTime);
            const selectedRateIndex = selectedMatch.rates.indexOf(rate);
            let betIndex = this.bet.findIndex(b => b.match === match && b.matchTime === matchTime);
            if(betIndex === -1){
                this.bet.push({
                    match: match,
                    matchTime: matchTime,
                    rate: rate,
                    rateIndex: selectedRateIndex,
                });
            }else{
                this.bet[betIndex].rate = rate;
                this.bet[betIndex].rateIndex = selectedRateIndex;
            }
            this.calculateTotalRate();
            
        },
        calculateTotalRate(){
            this.totalRate = this.bet.reduce((total, coupon) => total * coupon.rate, 1);
            this.predictedWin = this.selectedCross * this.totalRate;
            this.predictedWin = this.predictedWin.toFixed(2);
            this.totalRate = this.totalRate.toFixed(2);
        },
    },
    components: {
      matchInfo,
        couponItem
    }
};
</script>