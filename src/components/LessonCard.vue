<template>
  <div class="col-md-4 mb-4">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">
          <i :class="lesson.icon"></i> {{ lesson.subject }}
        </h5>
        <p class="card-text">
          <strong>Location:</strong> {{ lesson.location }} <br />
          <strong>Price:</strong> ${{ lesson.price }} <br />
          <strong>Spaces Left:</strong> {{ lesson.spaces }}
        </p>

        <!------add to cart ------->
        <button class="btn btn-success" @click="addToCart(lesson)">
          Add to Cart
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    lesson: Object
  },
  methods: {
    addToCart(lesson) {
      this.$emit('add-to-cart', lesson);
    }
  }
};
</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  border-radius: 8px;
}
</style>
