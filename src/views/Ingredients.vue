<template>
  <div class="p-8 bg-gradient-to-r from-teal-300 to-indigo-400 rounded-lg shadow-lg">
    <h1 class="text-5xl font-extrabold text-white text-center mb-8">Ingredients</h1>
  </div>

  <div class="px-8 py-4">
    <input
      type="text"
      v-model="keyword"
      class="rounded-lg border-2 bg-white border-gray-200 focus:ring-2 focus:ring-orange-500 focus:border-orange-500 mb-6 w-full px-4 py-2"
      placeholder="Search for Ingredients"
    />
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
      <a
        href="#"
        @click.prevent="openIngredient(ingredient)"
        v-for="ingredient of computedIngredients"
        :key="ingredient.idIngredient"
        class="bg-white rounded-xl p-6 shadow-md hover:shadow-xl transition-all transform hover:scale-105"
      >
        <h3 class="text-xl font-semibold text-gray-800 mb-3">{{ ingredient.strIngredient }}</h3>
      </a>
    </div>
  </div>
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { onMounted, ref } from "vue";
import { useRouter } from "vue-router";
import axiosClient from "../axiosClient";
import store from "../store";

const router = useRouter();
const keyword = ref("");
const ingredients = ref([]);
const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) =>
    i.strIngredient.toLowerCase().includes(keyword.value.toLowerCase())
  );
});

function openIngredient(ingredient) {
  store.commit('setIngredient', ingredient);
  router.push({
    name: "byIngredient",
    params: { ingredient: ingredient.strIngredient },
  });
}

onMounted(() => {
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>

<style scoped>
h1 {
  font-family: 'Lobster', cursive;
  letter-spacing: 2px;
}

input[type="text"] {
  font-size: 1.125rem;
  font-weight: 500;
}

a {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
  background-color: #f9fafb;
  border-radius: 12px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
}

a:hover {
  background-color: #fef6f3;
  transform: scale(1.05);
}

a h3 {
  color: #333;
  text-align: center;
}
</style>
