<template>
<baseHeader/>
<header class="header"> Merhabalar Hocam, "CSS CLASS APP", "COURSE PLANNER" ve Opsiyonel olan ve tum konulari iceren "BET COUPON" uygulamasini yaptim.. kalanlari yapamama sebebim bazi durumlardan dolayi zamanim olmadi.. mazuratimi affedin.. </header>
<component :is="currentView" />
</template>

<script>

import baseHeader from './components/share/baseHeader.vue';
import examOne from './components/rooting/examOne.vue';
import examTwo from './components/rooting/examTwo.vue';
//import examThree from './components/rooting/examThree.vue';
//import examFour from './components/rooting/examFour.vue';
//import examFive from './components/rooting/examFive.vue';
import examSix from './components/rooting/examSix.vue';

const rootes = {
  '/examOne': examOne,
  '/examTwo': examTwo,
  //'/examThree': examThree,
  //'/examFour': examFour,
  //'/examFive': examFive,
  '/examSix': examSix,
}

export default {
  data() {
    return {
      currentPath: window.location.hash,  
    }
  },
  
  components: {
    baseHeader  
  },
  computed:{
    currentView() {
      return rootes[this.currentPath.slice(1) || '/examOne' || '/examTwo' || '/examSix'];
    }
  },

  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
  } 
}
</script>

<style>
@import '../assets/app.css';
</style>
