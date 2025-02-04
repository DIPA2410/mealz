<template>
  <div class="bg-white shadow-lg rounded-xl hover:scale-105 transition-all transform duration-300 ease-in-out">
    <router-link :to="{ name: 'mealDetails', params: { id: meal.idMeal } }">
      <img
        :src="meal.strMealThumb"
        :alt="meal.strMeal"
        class="rounded-t-xl w-full h-48 object-cover shadow-md"
      />
    </router-link>
    <div class="p-4">
      <h3 class="font-semibold text-xl text-gray-800 mb-2">{{ meal.strMeal }}</h3>
      <p class="text-sm text-gray-600 mb-4">
        {{ $filters.truncateWords(meal.strInstructions, 20) }}
      </p>
      <div class="flex items-center justify-between">
        <YouTubeButton :href="meal.strYoutube" />
        <span class="text-sm text-gray-500">{{ meal.strCategory }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import YouTubeButton from './YouTubeButton.vue';

const { meal } = defineProps({
  meal: {
    required: true,
    type: Object
  }
})
</script>

<style scoped>
/* Hover and transition effects */
div:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease-in-out;
}

/* Card styling */
div {
  background-color: #ffffff;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

/* Text and layout tweaks */
h3 {
  font-weight: 600;
  color: #333;
}

p {
  color: #6B7280;
  font-size: 0.875rem; /* smaller text */
}

/* Add padding inside card */
div.p-4 {
  padding: 16px;
}

/* YouTube button styling */
YouTubeButton {
  background-color: #FF4500; /* Adjust color for visibility */
  color: white;
  border-radius: 50%;
  padding: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

YouTubeButton:hover {
  background-color: #FF6347;
}

/* Category text styling */
span {
  color: #A0AEC0; /* Light gray text */
  font-size: 0.875rem;
}
</style>
