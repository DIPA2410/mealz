<template>
  <div class="max-w-[800px] mx-auto p-8 bg-white rounded-lg shadow-lg mt-6">
    <h1 class="text-4xl font-extrabold text-orange-500 text-center mb-6">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="w-full rounded-lg shadow-md mb-6">

    <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 text-lg mb-6">
      <div class="flex flex-col">
        <strong class="font-semibold text-gray-700">Category:</strong>
        <span class="text-gray-600">{{ meal.strCategory }}</span>
      </div>
      <div class="flex flex-col">
        <strong class="font-semibold text-gray-700">Area:</strong>
        <span class="text-gray-600">{{ meal.strArea }}</span>
      </div>
      <div class="flex flex-col">
        <strong class="font-semibold text-gray-700">Tags:</strong>
        <span class="text-gray-600">{{ meal.strTags }}</span>
      </div>
    </div>

    <div class="my-4 text-gray-700 leading-relaxed">
      <p>{{ meal.strInstructions }}</p>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 gap-6 mb-6">
      <div>
        <h2 class="text-2xl font-semibold text-gray-800 mb-4">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)" :key="ind">
            <li v-if="meal[`strIngredient${ind + 1}`]" class="text-gray-600 mb-2">
              {{ ind + 1 }}. {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold text-gray-800 mb-4">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)" :key="ind">
            <li v-if="meal[`strMeasure${ind + 1}`]" class="text-gray-600 mb-2">
              {{ ind + 1 }}. {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
    </div>

    <div class="mt-4 flex justify-center gap-4">
      <YouTubeButton :href="meal.strYoutube" class="px-4 py-2 bg-red-600 text-white rounded-lg hover:bg-red-700 transition-all">
        Watch on YouTube
      </YouTubeButton>
      <a
        :href="meal.strSource"
        target="_blank"
        class="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 transition-all"
      >
        View Original Source
      </a>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router';
import axiosClient from '../axiosClient';
import YouTubeButton from '../components/YouTubeButton.vue';

const route = useRoute();
const meal = ref({})

onMounted(() => {
  axiosClient.get(`lookup.php?i=${route.params.id}`)
    .then(({ data }) => {
      meal.value = data.meals[0] || {}
    })
})
</script>

<style scoped>
/* Apply smoother transitions to links and buttons */
a, .hover\:bg-red-700:hover, .hover\:bg-indigo-700:hover {
  transition: background-color 0.3s ease;
}

/* Add a slight shadow to the images for better focus */
img {
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Apply rounded corners and shadow to the container */
div.max-w-[800px] {
  border-radius: 12px;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
}

/* Text styling for headings */
h1, h2 {
  font-family: 'Lobster', cursive;
}

h2 {
  font-size: 1.5rem;
}

/* Add padding and spacing for ingredient list items */
ul li {
  padding-left: 10px;
  margin-bottom: 6px;
}
</style>
