<template>
    <div class="container">
      <div class="course--planner-app--container">
        <div class="card">
          <inputZone @add-course="addCourse"/>
        </div>
        <div class="card card-light mt-20">
          <h3>Aktif Kurslarım</h3>
          <ul class="list mt-20">
            <todoRow class="course-item list-item bg-success" v-for="course in courses" :name="course.name" :isActive="course.isActive" @change-status="toggleCourse" :key="course.name"></todoRow>
          </ul>
        </div>
        <div class="mt-10" id="result-message">
          <small>Tamamlanan Kurs Sayısı:{{this.courses.filter((c)=>c.isActive).length}}</small>
          <br>
          <small>Bekleyen Kurs Sayısı:{{this.courses.filter((c)=>!c.isActive).length}}</small>
        </div>
      </div>
    </div>
</template>


<script>
import inputZone from '../exampleTwo/inputZone.vue';
import todoRow from '../exampleTwo/todoRow.vue';
export default {
  data() {
    return {
      courses: []
    };
  },
  methods: {
    toggleCourse(name) {
      const index = this.courses.findIndex(course => course.name == name);
      this.courses.at(index).isActive = !this.courses.at(index).isActive;
    },
    addCourse(name) {
      this.courses.push({
        name: name,
        isActive: false,
      });
    },
  },
  components: {
    inputZone,
    todoRow,
  }
}
</script>
