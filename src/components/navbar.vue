<template>
  <header class="bg-gradient-to-r from-pink-500 to-purple-600 shadow-lg h-16 flex justify-between items-center px-5 rounded-xl">
    <!-- Home Link without hover background and active background -->
    <router-link
      :to="{ name: 'home' }"
      class="inline-flex items-center px-4 py-2 h-full text-white font-bold text-xl transition-all duration-200 ease-in-out rounded-lg"
    >
      Home
    </router-link>

    <!-- Navigation Links -->
    <div class="flex items-center gap-10"> <!-- Increased gap between links -->
      <router-link
        :to="{ name: 'byName' }"
        class="inline-flex items-center px-4 py-2 h-full transition-all duration-200 ease-in-out text-white rounded-lg hover:bg-yellow-400 hover:text-black"
        active-class="bg-yellow-400 text-black"
      >
        Search Meals
      </router-link>
      <router-link
        :to="{ name: 'byLetter' }"
        class="inline-flex items-center px-4 py-2 h-full transition-all duration-200 ease-in-out text-white rounded-lg hover:bg-yellow-400 hover:text-black"
        active-class="bg-yellow-400 text-black"
      >
        Meals By Letter
      </router-link>
      <router-link
        :to="{ name: 'ingredients' }"
        class="inline-flex items-center px-4 py-2 h-full transition-all duration-200 ease-in-out text-white rounded-lg hover:bg-yellow-400 hover:text-black"
        active-class="bg-yellow-400 text-black"
      >
        Meals By Ingredients
      </router-link>
    </div>
  </header>
</template>

<style scoped>
/* Adding a subtle shadow to the header for depth */
header {
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.1);
}

/* Remove background color for active Home link */
.router-link-exact-active {
  background-color: transparent; /* No background for Home link */
}

/* For the hover effect on nav items */
.router-link-active {
  background-color: rgba(255, 255, 255, 0.1); /* Light background on active state */
  color: white;
}

/* Adding transitions to the text color and background */
.router-link-exact-active,
.router-link-active {
  transition: background-color 0.2s, color 0.2s;
}

/* Add a smooth transition effect when hovering over the navbar */
a:hover {
  transition: background-color 0.3s ease, transform 0.3s ease;
  transform: translateY(-3px);
}
</style>
