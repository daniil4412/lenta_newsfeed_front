<script setup>
import { ref } from 'vue'
import BaseInput from '../components/BaseInput.vue'
import BaseButton from '../components/BaseButton.vue'
import BaseToggle from '../components/BaseToggle.vue'
import BaseImageUpload from '../components/BaseImageUpload.vue'

const testEmail = ref('')
const testPassword = ref('')
const activeTab = ref('login') 
const testImages = ref([])
</script>

<template>
  <div style="padding: 50px; display: flex; flex-direction: column; align-items: center;">
    
    <BaseToggle 
      v-model="activeTab" 
      :options="[
        { label: 'Вход', value: 'login' },
        { label: 'Регистрация', value: 'register' }
      ]" 
    />

    <BaseInput v-model="testEmail" label="Email" type="email" id="email" />
    <BaseInput v-model="testPassword" label="Пароль" type="password" id="password" />
    
    <div style="display: flex; gap: 10px; margin: 20px 0;">
      <BaseButton class="btn-register">Регистрация</BaseButton>
      <BaseButton class="btn-standard">Отправить код</BaseButton>
      <BaseButton class="btn-delete">Удалить</BaseButton>
    </div>

    <div style="margin-top: 20px;">
      <p>Загрузка обложек:</p>
      <BaseImageUpload v-model="testImages" />
    </div>

  </div>
</template>