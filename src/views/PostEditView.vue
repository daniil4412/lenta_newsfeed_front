<script setup>
import { ref, computed } from 'vue'
import BaseInput from '../components/BaseInput.vue'
import BaseButton from '../components/BaseButton.vue'
import BaseImageUpload from '../components/BaseImageUpload.vue'

// Поля из API
const title = ref('')
const topic = ref('')
const text = ref('')
const images = ref([]) // Массив загруженных картинок

// Валидация: кнопка активна, если заполнены Название и Текст
const isFormValid = computed(() => {
  return title.value.trim().length > 3 && text.value.trim().length > 10
})

const savePost = () => {
  if (!isFormValid.value) return

  // ЗДЕСЬ БУДЕТ ЗАПРОС К API (POST /posts или PUT /posts/[id])
  // по API мы передаем имена файлов, а не сами файлы
  const imageNames = images.value.map(img => img.file.name)

  console.log('Отправка на сервер:', {
    title: title.value,
    topic: topic.value,
    text: text.value,
    images: imageNames
  })
  
  alert('Пост сохранен! (имитация)')
}
</script>

<template>
  <div class="edit-page">
    <div class="form-container">
      
      <div class="form-group">
        <BaseInput 
          v-model="title" 
          label="Название" 
          id="title"
        />
      </div>

      <div class="form-group">
        <BaseInput 
          v-model="topic" 
          label="Тема"  
          id="topic"
        />
      </div>

      <div class="form-group">
        <label class="label-text">Иллюстрации</label>
        <!-- Компонент загрузки картинок -->
        <BaseImageUpload v-model="images" />
      </div>

      <div class="form-group">
        <label class="label-text">Текст</label>
        <textarea 
          v-model="text" 
          class="base-textarea" 
          rows="6"
        ></textarea>
      </div>

      <div class="submit-wrapper">
        <!-- Кнопка "Сохранить" -->
        <BaseButton 
          class="btn-standard" 
          :disabled="!isFormValid" 
          @click="savePost"
        >
          Сохранить
        </BaseButton>
      </div>

    </div>
  </div>
</template>

<style scoped>
.edit-page {
  padding: 40px 20px;
  display: flex;
  justify-content: center;
}

.form-container {
  background: white;
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0,0,0,0.05);
  width: 100%;
  max-width: 500px;
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
}

.label-text {
  font-size: 14px;
  color: #666;
  margin-bottom: 8px;
  font-weight: bold;
}

/* Стилизация textarea под общий дизайн */
.base-textarea {
  background-color: #e5e5e5;
  border: none;
  border-radius: 8px;
  padding: 12px 15px;
  font-size: 16px;
  outline: none;
  width: 100%;
  resize: vertical;
  font-family: inherit;
  color: #333;
}

.base-textarea:focus {
  box-shadow: 0 0 0 2px #a855f7; /* Фиолетовая обводка при клике */
}

.submit-wrapper {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
</style>