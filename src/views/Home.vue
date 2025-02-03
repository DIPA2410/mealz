<template>
  <div class="p-8 pb-0 bg-gradient-to-r from-sky-400 to-blue-600 rounded-lg shadow-lg">
    <h1 class="text-5xl font-extrabold text-white mb-8 text-center">Random Meals</h1>
    <!-- Add a margin bottom to the letters section to create space from the bottom -->
  <div class="flex flex-wrap justify-center gap-4 px-8 mb-8">
    <router-link
      :to="{ name: 'byLetter', params: { letter } }"
      v-for="letter of letters"
      :key="letter"
      class="w-12 h-12 flex items-center justify-center bg-white text-2xl font-semibold rounded-full text-sky-600 hover:bg-sky-100 hover:text-blue-500 hover:scale-125 transition-all shadow-md"
    >
      {{ letter }}
    </router-link>
  </div>
  </div>
  <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-6">
      <div
        v-for="meal in meals"
        :key="meal.idMeal"
        class="meal-card bg-white rounded-lg overflow-hidden shadow-lg flex flex-col"
      >
        <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
          <img
            :src="meal.strMealThumb"
            :alt="meal.strMeal"
            class="meal-image w-full"
          />
        </router-link>
        <div class="meal-content p-4 flex-grow">
          <h3 class="meal-title font-semibold text-xl text-gray-800 mb-2">{{ meal.strMeal }}</h3>
          <p class="meal-description text-gray-600">{{ meal.strInstructions.substring(0, 80) }}...</p>
        </div>
      </div>
    </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import axiosClient from "../axiosClient.js";

const meals = ref([]);

onMounted(async () => {
  for (let i = 0; i < 10; i++) {
    axiosClient
      .get(`random.php`)
      .then(({ data }) => meals.value.push(data.meals[0]));
  }
});
</script>

<style scoped>
/* Header background gradient */
div.p-8 {
  background: linear-gradient(to right, #55e4ee, #7499f6); /* Skyblue to Darker Blue */
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Centered title with white text */
h1 {
  font-family: 'Lobster', cursive;
  letter-spacing: 2px;
  color: #ffffff; /* White text */
}

/* Meal card styles */
.meal-card {
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  height: 350px; /* Fixed height for consistency */
  display: flex;
  flex-direction: column;
}

.meal-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.2);
}

/* Meal image styles */
.meal-image {
  border-top-left-radius: 12px;
  border-top-right-radius: 12px;
  height: 180px;
  object-fit: cover;
}

/* Meal content styling */
.meal-content {
  padding: 1rem;
  flex-grow: 1;
}

.meal-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #333;
  margin-bottom: 0.5rem;
}

.meal-description {
  font-size: 0.875rem;
  color: #777;
}
</style>
