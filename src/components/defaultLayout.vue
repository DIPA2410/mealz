<template>
  <div class="min-h-screen bg-gradient-to-r from-teal-50 to-pink-100">
    <Navbar />
    <main class="py-8">
      <div class="max-w-[1200px] mx-auto bg-white p-6 rounded-lg shadow-lg">
        <router-view />
      </div>
    </main>
  </div>
</template>

<script setup>
import Navbar from "../components/Navbar.vue";
</script>

<style scoped>
/* Background gradient for the entire page */
div {
  background: linear-gradient(to right, #e0f7fa, #f8bbd0);
}

/* Styling for the main content container */
main {
  padding-top: 40px;
}

/* Adding a subtle shadow and rounded corners to the main content box */
div.max-w-[1200px] {
  background-color: #ffffff;
  border-radius: 15px;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.1);
}

/* Smooth transition for the content */
main .router-view {
  transition: opacity 0.3s ease;
}
</style>
