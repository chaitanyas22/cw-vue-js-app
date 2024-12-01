<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">After School Activities</h1>
    <div class="d-flex justify-content-end mb-3">
      <label for="sort" class="mr-2">Sort By:</label>
      <select v-model="sortAttribute" class="form-control w-auto mr-2" @change="sortLessons">
        <option value="subject">Subject</option>
        <option value="location">Location</option>
        <option value="price">Price</option>
        <option value="spaces">Spaces</option>
      </select>
      <button class="btn btn-primary" @click="toggleSortOrder">
        {{ sortOrder === 'asc' ? 'Ascending' : 'Descending' }}
      </button>
    </div>
    <div class="row">
      <LessonCard
        v-for="lesson in lessons"
        :key="lesson.id"
        :lesson="lesson"
      />
    </div>
  </div>
</template>

<script>
import LessonCard from './components/LessonCard.vue';

export default {
  name: 'App',
  components: {
    LessonCard,
  },
  data() {
    return {
      lessons: [
        { id: 1, subject: 'Math', location: 'Room A', price: 10, spaces: 5, icon: 'fas fa-calculator' },
        { id: 2, subject: 'Science', location: 'Room B', price: 15, spaces: 3, icon: 'fas fa-flask' },
        // Add at least 10 lessons
      ],
      sortAttribute: 'subject',
      sortOrder: 'asc',
    };
  },
  methods: {
    sortLessons() {
      const order = this.sortOrder === 'asc' ? 1 : -1;
      this.lessons.sort((a, b) =>
        a[this.sortAttribute] > b[this.sortAttribute] ? order : -order
      );
    },
    toggleSortOrder() {
      this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc';
      this.sortLessons();
    },
  },
};
</script>

<style scoped>
h1 {
  color: #4CAF50;
}
</style>
