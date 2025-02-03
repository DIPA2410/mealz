<template>
  <div class="p-8 pb-0 bg-gradient-to-r from-teal-50 to-orange-100 rounded-lg shadow-lg">
    <h1 class="text-4xl font-extrabold text-orange-500 text-center mb-6">Meals for {{ ingredient.strIngredient }}</h1>
  </div>

  <div class="px-8">
    <Meals :meals="meals" />
  </div>
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import store from "../store";
import Meals from '../components/Meals.vue'

const route = useRoute();
const ingredient = computed(() => store.state.ingredient)
const meals = computed(() => store.state.mealsByIngredient)

onMounted(() => {
  store.dispatch('searchMealsByIngredient', route.params.ingredient)
})
</script>

<style scoped>
/* Background gradient for the header */
div.p-8 {
  background: linear-gradient(to right, #d0f2f1, #ffedd5);
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Centering the title */
h1 {
  text-align: center;
  font-family: 'Lobster', cursive;
  color: #f97316; /* Orange color */
}

/* Meals section styling */
div.px-8 {
  padding-top: 20px;
}

/* Subtle hover effect for each meal */
.meal-card {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}
.meal-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
}
</style>
