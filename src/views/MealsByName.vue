<template>
  <div class="p-8 pb-0 bg-gradient-to-r from-sky-400 to-blue-600 rounded-lg shadow-lg">
    <h1 class="text-4xl font-extrabold text-white text-center mb-6">Search Meals by Name</h1>
  </div>

  <div class="px-8 pb-6">
    <input
      type="text"
      v-model="keyword"
      class="rounded-full border-2 bg-white border-gray-200 focus:ring-orange-500 focus:border-orange-500 py-3 px-6 w-full shadow-md transition-all"
      placeholder="Search for Meals"
      @change="searchMeals"
    />
  </div>

  <Meals :meals="meals" />
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from "../components/Meals.vue";

const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  if (keyword.value) {
    store.dispatch("searchMeals", keyword.value);
  } else {
    store.commit("setSearchedMeals", []);
  }
}

onMounted(() => {
  keyword.value = route.params.name;
  if (keyword.value) {
    searchMeals();
  }
});
</script>

<style scoped>
/* Header background gradient */
div.p-8 {
  background: linear-gradient(to right, #55e4ee, #7499f6); /* Skyblue to Darker Blue gradient */
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  padding-bottom: 40px; /* Added space for the input section */
}

/* Centered title with white text */
h1 {
  font-family: 'Lobster', cursive;
  color: #ffffff; /* White text */
}

/* Search input field styling */
input[type="text"] {
  background-color: #ffffff;
  color: #333333;
  border-radius: 50px;
  border: 2px solid #e5e7eb;
  padding: 12px 20px;
  font-size: 1.125rem;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

input[type="text"]:focus {
  border-color: #f97316; /* Focus color */
  box-shadow: 0 4px 12px rgba(255, 165, 0, 0.2);
}

/* Meal section padding */
div.px-8 {
  padding-top: 20px;
}

/* Hover effect for meal cards */
.meal-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.meal-card:hover {
  transform: translateY(-8px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.1);
}
</style>
