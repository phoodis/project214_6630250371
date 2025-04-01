<script setup>
 import { RouterLink, RouterView } from 'vue-router'
 import Home from './views/HomeView.vue'
 import Info from './views/InfoView.vue'
 
</script>

<template>
   <nav>
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/info">Information</RouterLink>
  </nav>
  <RouterView />
</template>

<style scoped>
nav {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  background-color: #0073e6; /* สีพื้นหลัง */
  padding: 15px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
  border-radius: 10px;
  margin: 20px auto;
  max-width: 500px;
}

nav a {
  text-decoration: none;
  color: white;
  font-size: 18px;
  font-weight: bold;
  padding: 10px 15px;
  border-radius: 8px;
  transition: all 0.3s ease-in-out;
}

nav a:hover {
  background-color: #005bb5;
  transform: scale(1.1);
}

/* ทำให้ responsive บนจอเล็ก */
@media (max-width: 500px) {
  nav {
    flex-direction: column;
    gap: 10px;
    padding: 10px;
  }

  nav a {
    font-size: 16px;
    padding: 8px 12px;
  }
}
</style>
