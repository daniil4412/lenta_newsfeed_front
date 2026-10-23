<script setup>
import { ref } from 'vue'
import { RouterView } from 'vue-router'
import SidebarMenu from './components/SidebarMenu.vue'

// Логика для мобильного меню
const isMenuOpen = ref(false)
</script>

<template>
  <div class="app-wrapper">
    <!-- Временная шапка для мобилки -->
    <header class="mobile-header">
      <button class="burger-btn" @click="isMenuOpen = !isMenuOpen">☰</button>
      <span>ЛЕНТА НОВОСТЕЙ</span>
    </header>

    <div class="main-layout">
      <!-- Панель слева -->
      <SidebarMenu :class="{ 'open': isMenuOpen }" />
      
      <!-- Контент (ваши формы) -->
      <main class="content">
        <RouterView />
      </main>
    </div>
    
    <!-- Затемнение -->
    <div v-if="isMenuOpen" class="overlay" @click="isMenuOpen = false"></div>
  </div>
</template>

<style>
body { margin: 0; padding: 0; background-color: #f5f5f5; }
.app-wrapper { display: flex; flex-direction: column; min-height: 100vh; }

.mobile-header {
  display: none;
  background: #5b21b6;
  color: white;
  padding: 10px 20px;
  align-items: center;
  gap: 15px;
  font-weight: bold;
}

.burger-btn {
  background: none; border: none; color: white; font-size: 24px; cursor: pointer;
}

.main-layout { display: flex; flex: 1; }
.content { flex: 1; padding: 20px; }

.overlay {
  position: fixed; top: 0; left: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.5); z-index: 999;
}

@media (max-width: 767px) {
  .mobile-header { display: flex; }
}
</style>