<script setup>
import { ref } from 'vue'
import BaseModal from './BaseModal.vue'

const activeSection = ref('all')
const toggleSection = (section) => {
  activeSection.value = activeSection.value === section ? '' : section
}

const isLogoutModalOpen = ref(false)

// =========================================================================
// ЗАГЛУШКА (логика выхода)
// =========================================================================
const handleLogout = () => {
  console.log('Пользователь вышел из системы (имитация)')
  isLogoutModalOpen.value = false 
}
</script>

<template>
  <aside class="sidebar">
    <div class="menu-content">
      <!-- Раздел 1: Все посты -->
      <div class="menu-section">
        <h3 class="section-title" @click="toggleSection('all')" :class="{ active: activeSection === 'all' }">
          Все посты
        </h3>
        <ul v-if="activeSection === 'all'" class="sub-menu">
          <!-- ========================================================= -->
          <!-- ЗАГЛУШКА ДЛЯ СПИСКА ТЕМ (Верстка)                       -->
          <!-- ========================================================= -->
          <li class="sub-item placeholder">Список тем загружается...</li>
        </ul>
      </div>

      <!-- Раздел 2: Мои посты -->
      <div class="menu-section">
        <h3 class="section-title" @click="toggleSection('my')" :class="{ active: activeSection === 'my' }">
          Мои посты
        </h3>
        <ul v-if="activeSection === 'my'" class="sub-menu">
          <!-- ========================================================= -->
          <!-- ЗАГЛУШКА ДЛЯ СПИСКА МОИХ ПОСТОВ (Верстка)               -->
          <!-- ========================================================= -->
          <li class="sub-item placeholder">Список ваших постов...</li>
        </ul>
      </div>

      <!-- Раздел 3: Модерация постов -->
      <div class="menu-section">
        <h3 class="section-title" @click="toggleSection('moderation')" :class="{ active: activeSection === 'moderation' }">
          Модерация постов
        </h3>
        <ul v-if="activeSection === 'moderation'" class="sub-menu">
          <!-- ========================================================= -->
          <!-- ЗАГЛУШКА ДЛЯ СПИСКА ПОСТОВ НА МОДЕРАЦИИ (Верстка)       -->
          <!-- ========================================================= -->
          <li class="sub-item placeholder">Постов на модерации нет</li>
        </ul>
      </div>

      <!-- КНОПКА ВЫХОДА (теперь идет сразу после списка) -->
      <div class="logout-section">
        <button class="logout-btn" @click="isLogoutModalOpen = true">
          Выйти из аккаунта
        </button>
      </div>
    </div>

    <!-- Окно подтверждения -->
    <BaseModal 
      :is-open="isLogoutModalOpen" 
      title="Выход из аккаунта"
      @close="isLogoutModalOpen = false"
      @confirm="handleLogout"
    >
      Вы действительно хотите выйти из своего аккаунта?
    </BaseModal>

  </aside>
</template>

<style scoped>
.sidebar {
  width: 250px;
  font-family: 'Montserrat', sans-serif;
  background-color: white;
  height: 100%;
}

.menu-content {
  padding: 20px;
}

/* Стили разделов (без изменений) */
.menu-section { margin-bottom: 15px; }
.section-title { font-size: 16px; font-weight: 700; color: #333; cursor: pointer; padding: 8px 0; margin: 0; transition: color 0.2s; }
.section-title:hover, .section-title.active { color: #ff8000; }
.sub-menu { list-style: none; padding: 0; margin: 5px 0 0 0; }
.sub-item { font-size: 14px; color: #666; padding: 6px 0 6px 15px; cursor: pointer; border-left: 2px solid transparent; transition: all 0.2s; }
.sub-item:hover { color: #ff8000; border-left-color: #ff8000; }
.placeholder { color: #aaa; font-style: italic; cursor: default; }
.placeholder:hover { color: #aaa; border-left-color: transparent; }

/* Стили для кнопки выхода */
.logout-section {
  margin-top: 25px; /* Отступ сверху, чтобы отделить от списков */
}

.logout-btn {
  width: 100%;
  padding: 10px;
  background: transparent;
  border: 1px solid #ff8000;
  color: #ff8000;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s;
}

.logout-btn:hover {
  background: #ff8000;
  color: white;
}

/* --- АДАПТИВНОСТЬ --- */
@media (min-width: 768px) {
  .sidebar { display: block; border-right: 1px solid #eee; height: 100vh; position: sticky; top: 0; }
}

@media (max-width: 767px) {
  .sidebar {
    position: fixed;
    top: 0;
    left: 0;
    height: 100vh;
    z-index: 1000;
    transform: translateX(-100%);
    transition: transform 0.3s ease;
    box-shadow: 2px 0 10px rgba(0,0,0,0.1);
  }
  .sidebar.open { transform: translateX(0); }
}
</style>