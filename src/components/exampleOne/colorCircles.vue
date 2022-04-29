<template>
    <li v-for="color in colors" :style="{ backgroundColor: color }" @click="setColor" :key="{color}"></li>
</template>

<script>

export default {
    props:{
        colors: Array,
        setColor: Function
    }
}
</script>
