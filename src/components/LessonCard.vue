<template>
  <div class="col-md-4 mb-3">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">
          <i :class="lesson.icon"></i> {{ lesson.subject }}
        </h5>
        <p class="card-text">Location: {{ lesson.location }}</p>
        <p class="card-text">Price: ${{ lesson.price }}</p>
        <p class="card-text">Spaces Left: {{ lesson.spaces }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LessonCard',
  props: {
    lesson: Object,
  },
};
</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  border-radius: 5px;
}
.card-title {
  font-weight: bold;
}
</style>
