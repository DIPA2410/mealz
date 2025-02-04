<template>
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-5 px-8">
    <!-- Meal Items Grid -->
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>

  <!-- No Meals Available Message -->
  <div v-if="!meals.length" class="flex justify-center items-center text-gray-600 p-8">
    <p class="text-xl font-semibold">There are no meals available</p>
  </div>
</template>

<script setup>
import MealItem from './MealItem.vue';

const { meals } = defineProps({
  meals: {
    required: true,
    type: Array,
  }
})
</script>

<style scoped>
/* Adjust grid layout for responsiveness */
.grid {
  gap: 1.25rem; /* Increase gap for better spacing */
}

/* Centered message styling */
.flex {
  font-size: 1.125rem; /* Slightly larger text for better visibility */
  text-align: center;
}

.text-gray-600 {
  color: #4B5563; /* Slightly darker gray for better contrast */
}
</style>
