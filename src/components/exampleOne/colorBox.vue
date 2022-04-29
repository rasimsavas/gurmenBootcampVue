<template>
    <div class="result-box" :style="{ backgroundColor : color }">  </div>
</template>


<script>

export default {
    props:{
        color: String,
        isColor: Boolean
    }
}

</script>
