
<template>
  <div class="card m-3" style="width: 18rem;">

    <i :class="lesson.icon" class="card-img-top fa-4x text-center py-3"></i>

    <div class="card-body">
      <h5 class="card-title">{{ lesson.subject }}</h5>
      <p class="card-text">Location: {{ lesson.location }}</p>

      <p class="card-text">Price: ${{ lesson.price }}</p>
      <p class="card-text">Spaces: {{ lesson.spaces }}</p>
      <button 

        class="btn btn-primary"
        @click="$emit('add-to-cart', lesson)"
        :disabled="lesson.spaces < 1" >
        Add to Cart
      </button>
    </div>
  </div>

</template>

<script>
export default {
  name: "LessonCard",
  
  props: {
    lesson: Object,
  },
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  transition: 0.3s;
}
.card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}
</style>
