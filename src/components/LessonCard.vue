<template>
  <div class="col-md-4 mb-4">
    <div class="card">
      <div class="card-body">
        <i :class="lesson.icon" style="font-size: 2rem;"></i>
        <h5 class="card-title">{{ lesson.subject }}</h5>
        <p class="card-text">Location: {{ lesson.location }}</p>
        <p class="card-text">Price: ${{ lesson.price }}</p>
        <p class="card-text">Spaces Left: {{ lesson.spaces }}</p>

        <!-----add to cart button -->
        <button
          class="btn btn-success"
          @click="addToCart"
          :disabled="lesson.spaces === 0"
        >
          Add to Cart
        </button>
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
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.lesson);
    },
  },
};
</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
}
</style>
