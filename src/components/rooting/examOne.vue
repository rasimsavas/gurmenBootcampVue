
<template>
    <div class="container css--class--app">
      <div class="card text-center">
        <ul class="css--palette text-center">
          <colorCircles :colors="colors" :setColor="setColor" :key="colors"></colorCircles>
        </ul>
        <colorBox :color="getColor()"> </colorBox>
      </div>
    </div>
</template>


<script>
import colorBox from '../exampleOne/colorBox.vue';
import colorCircles from '../exampleOne/colorCircles.vue';

export default {
  data() {
    return {
      selectedColor: '#000000',
      colors: ['red', 'green', 'blue']
    }
    },
    methods:{
      setColor(event){
        console.log(event);
        this.selectedColor = event.target.style.backgroundColor;
      },
      getColor(){
        return this.selectedColor;
      }
    },
    components: {
        colorBox,
        colorCircles
    } 
}
</script>
