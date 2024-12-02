<!-- src/components/Lessons.vue -->
<template>
    <div>
      <h1>Lessons from the Backend</h1>
      <ul v-if="lessons.length">
        <li v-for="lesson in lessons" :key="lesson._id">
          {{ lesson.name }}: {{ lesson.description }}
        </li>
      </ul>
      <p v-else>Loading lessons...</p>


    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        lessons: []  // Array to store lessons data
      };
    },
    mounted() {
        
      // Fetch lessons data from your Express backend
      fetch('https://your-express-api-url/api/lessons')
        .then(response => response.json())
        .then(data => {
          this.lessons = data;  // Assign the fetched data to lessons array
        })
        .catch(error => {
          console.error('Error fetching lessons:', error);
        });
    }
  };
  </script>
  