<template>
  <div class="app">
    <header class="header">
      <nav class="nav-container">
        <router-link to="/" class="logo">
          <Newspaper class="logo-icon" />
          <span>InfoNews</span>
        </router-link>
        <div class="nav-links">
          <router-link to="/">Inicio</router-link>
          <router-link to="/categories">Categorías</router-link>
          <router-link to="/trending">Tendencias</router-link>
        </div>
        <button @click="toggleTheme" class="theme-toggle">
          <Sun v-if="isDarkMode" />
          <Moon v-else />
        </button>
      </nav>
    </header>
    <main class="main-content">
      <router-view v-slot="{ Component }">
        <transition name="fade" mode="out-in">
          <component :is="Component" />
        </transition>
      </router-view>
    </main>
    <footer class="footer">
      <p>&copy; 2024 InfoNews. Todos los derechos reservados.</p>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Newspaper, Sun, Moon } from 'lucide-vue-next'

const isDarkMode = ref(false)

const toggleTheme = () => {
  isDarkMode.value = !isDarkMode.value
  document.body.classList.toggle('dark-mode')
}
</script>

<style>
:root {
  --primary-color: #2563eb;
  --secondary-color: #3b82f6;
  --background-color: #ffffff;
  --text-color: #1f2937;
  --card-background: #f3f4f6;
  --border-color: #e5e7eb;
}

.dark-mode {
  --background-color: #1f2937;
  --text-color: #f3f4f6;
  --card-background: #374151;
  --border-color: #4b5563;
}

body {
  background-color: var(--background-color);
  color: var(--text-color);
  transition: background-color 0.3s, color 0.3s;
}

.app {
  max-width: 1200px;
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.header {
  background-color: var(--background-color);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 10;
}

.nav-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  font-size: 1.5rem;
  font-weight: bold;
  color: var(--primary-color);
}

.logo-icon {
  width: 24px;
  height: 24px;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-links a {
  color: var(--text-color);
  text-decoration: none;
  font-weight: 500;
  transition: color 0.2s;
}

.nav-links a:hover {
  color: var(--primary-color);
}

.theme-toggle {
  background: none;
  border: none;
  cursor: pointer;
  color: var(--text-color);
}

.main-content {
  flex: 1;
  padding: 2rem;
}

.footer {
  background-color: var(--card-background);
  padding: 1rem;
  text-align: center;
  margin-top: auto;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>