<template>
    <div class="user--action--container">
        <div class="form-group">
            <label>Kursun Adı</label>
            <input type="text" id="course-name-field" />
        </div>
        <button class="btn-primary" @click="this.addCourse()">Kurs Ekle</button>
    </div>
</template>

<script>
export default {
    methods: {
        getCourseName() {
            console.log(document.getElementById('course-name-field').value);
            return document.getElementById('course-name-field').value;
        },
        addCourse() {
            this.$emit('add-course', this.getCourseName());
        },
    },
};
</script>