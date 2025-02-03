<template>
  <div class="p-8 pb-0 bg-gradient-to-r from-sky-400 to-blue-600 rounded-lg shadow-lg">
    <h1 class="text-4xl font-extrabold text-white text-center mb-6">Meals by Letter</h1>
  </div>

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

  <div class="px-8">
    <Meals :meals="meals" />
  </div>
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { onMounted, watch } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from "../components/Meals.vue";

const route = useRoute();
const letters = "ABCDEFGHIJKLMNOPQRSTUVWXYZ".split("");
const meals = computed(() => store.state.mealsByLetter);

watch(route, () => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});

onMounted(() => {
  store.dispatch("searchMealsByLetter", route.params.letter);
});
</script>

<style scoped>
/* Header background gradient */
div.p-8 {
  background: linear-gradient(to right, #55e4ee, #7499f6); /* Skyblue to Darker Blue gradient */
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  /* Add padding to the bottom to create space for the letters section */
  padding-bottom: 40px;
}

/* Centered title with white text */
h1 {
  font-family: 'Lobster', cursive;
  color: #ffffff; /* White text color */
}

/* Styling the letter buttons */
.router-link-exact-active,
.router-link-active {
  background-color: #ffffff;
  color: #0ea5e9; /* Sky blue color */
}

.router-link-exact-active:hover,
.router-link-active:hover {
  background-color: #d1f7f3;
  color: #1f75d1; /* Dark blue for hover effect */
  scale: 1.2;
  transition: all 0.3s ease;
}

/* Meal section padding */
div.px-8 {
  padding-top: 20px;
}

/* Add margin to the letter section to give some space from the bottom */
div.flex {
  margin-bottom: 30px; /* Adjust as needed */
}

/* Hover effect for meal cards */
.meal-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.meal-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
}
</style>
