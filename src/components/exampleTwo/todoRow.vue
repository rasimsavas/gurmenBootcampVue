<template>
    <li class="course-item list-item" :class="(isActive ? 'bg-success': 'bg-danger')">
        <span>{{name}}</span>
        <input type="checkbox" :checked="isActive" @change="changeStatus">
    </li>
</template>

<script>
export default {
    data() {
        return {
            status: '',
        }
    },
    props: {
        name: String,
        isActive: Boolean,
    },
    methods: {
        changeStatus() {
            this.$emit('change-status', this.name);
        }
    },
};
</script>