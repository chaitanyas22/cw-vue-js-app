<template>
  <div class="container mt-5">
    <h1 class="text-center mb-4">After School Activities</h1>

    <!-- ---- Search Bar -->
    <div class="d-flex justify-content-between mb-3">

      <input
      
        type="text"
        v-model="searchQuery"
        class="form-control w-50"

        placeholder="Search for lessons"
      />
    </div>

    <!-- Sort Section -->



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

    <!---------------------- Lesson Cards -->
    <div class="row">
      <LessonCard
        v-for="lesson in filteredLessons"
        :key="lesson.id"
        :lesson="lesson"
        @add-to-cart="addToCart"
      />
    </div>

    <!-- add to cart -->

    <div class="cart mt-5">
      
      <h2>Cart</h2>
      <ul>
        <li v-for="item in cart" :key="item.id">
          {{ item.subject }} - {{ item.location }} - ${{ item.price }}

          <button class="btn btn-danger btn-sm ml-2" @click="removeFromCart(item.id)">
            Remove
          </button>
                   </li>   </ul>
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
  data() 
  {
    return {

      lessons: [
        { id: 1, subject: 'Math', location: 'Hendon', price: 10, spaces: 5, icon: 'fas fa-calculator' },
        { id: 2, subject: 'Science', location: 'Golders Green', price: 15, spaces: 3, icon: 'fas fa-flask' },
        { id: 3, subject: 'English', location: 'Oxford Street', price: 12, spaces: 4, icon: 'fas fa-book' },
        { id: 4, subject: 'History', location: 'Wembley', price: 18, spaces: 6, icon: 'fas fa-landmark' },
        { id: 5, subject: 'Geography', location: 'East Ham', price: 14, spaces: 2, icon: 'fas fa-globe' },
        { id: 6, subject: 'Art', location: 'Hounslow', price: 20, spaces: 5, icon: 'fas fa-palette' },
        { id: 7, subject: 'Music', location: 'Chancery Lane', price: 25, spaces: 3, icon: 'fas fa-music' },
        { id: 8, subject: 'Swimming', location: 'Brent Cross', price: 30, spaces: 8, icon: 'fas fa-swimmer' },
        { id: 9, subject: 'French', location: 'North Finchley', price: 22, spaces: 7, icon: 'fas fa-language' },
        { id: 10, subject: 'Spanish', location: 'Mile Hill', price: 16, spaces: 4, icon: 'fas fa-language' },
        { id: 11, subject: 'Computer Science', location: 'Uxbridge', price: 35, spaces: 5, icon: 'fas fa-laptop-code' },
        { id: 12, subject: 'Drama', location: 'Kent', price: 17, spaces: 6, icon: 'fas fa-theater-masks' },
        { id: 13, subject: 'Physical Education', location: 'Colindale', price: 28, spaces: 10, icon: 'fas fa-futbol' },
        { id: 14, subject: 'Cooking', location: 'Kingsbury', price: 20, spaces: 4, icon: 'fas fa-utensils' },
        { id: 15, subject: 'Photography', location: 'Harrow', price: 40, spaces: 2, icon: 'fas fa-camera' },
      ],

      sortAttribute: 'subject',
      sortOrder: 'asc',
      searchQuery: '',
      cart: [],
    };
  },
  computed: {
    filteredLessons() {
      const query = this.searchQuery.toLowerCase();
      
      return this.lessons.filter((lesson) =>
        Object.values(lesson).some((value) =>
          value.toString().toLowerCase().includes(query)
        )
      );
    },
  },
  methods: {
    sortLessons() {

      const order = this.sortOrder === 'asc' ? 1 : -1;
      this.lessons.sort((a, b) =>
        a[this.sortAttribute] > b[this.sortAttribute] ? order : -order
      );
    },
// sort function

    toggleSortOrder() {
      this.sortOrder = this.sortOrder === 'asc' ? 'desc' : 'asc';
      this.sortLessons();
    },
    // add to cart functionaliry
    addToCart(lesson) {
      if (!this.cart.find((item) => item.id === lesson.id)) {
        this.cart.push(lesson);
        lesson.spaces -= 1;
      } else {
        alert('This lesson is already in your cart.');
      }
    },

    // remove from cart FUnciton
    removeFromCart(lessonId) {
      const index = this.cart.findIndex((item) => item.id === lessonId);
      if (index !== -1) {
        const lesson = this.cart[index];
        lesson.spaces += 1;
        this.cart.splice(index, 1);
      }
    },
  },
};
</script>

<style scoped>
h1 {
  color: #4CAF50;
}
.cart {
  background: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
}
</style>
