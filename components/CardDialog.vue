<!-- CardDialog.vue -->
<template>
    <v-dialog v-model="dialogVisible">
      <v-card v-if="selectedCard">
        <v-card-title>{{ selectedCard.arrayName }}</v-card-title>
        <v-card-subtitle>ID: {{ selectedCard.arrayId }}</v-card-subtitle>
        <v-card-text>
          <div>Дата загрузки: {{ selectedCard.dateOfLoad }}</div>
          <div>Статус загрузки: {{ selectedCard.statusOfLoad ? 'Загружен' : 'Не загружен' }}</div>
          <div>Статус сортировки: {{ selectedCard.statusOfSorted ? 'Отсортирован' : 'Не отсортирован' }}</div>
          <div v-if="selectedCard.arrayData">Данные массива: {{ selectedCard.arrayData.join(', ') }}</div>
        </v-card-text>
        <v-card-actions>
          <!-- Используем ветвление для текста кнопки и метода при нажатии -->
          <v-btn @click="selectedCard.statusOfSorted ? showSortedArrayInfo : startSorting">
            {{ selectedCard.statusOfSorted ? 'Показать данные сортировки' : 'Начать сортировку' }}
          </v-btn>
          <v-btn @click="editArray">Изменить массив</v-btn>
          <v-btn @click="deleteArray">Удалить массив</v-btn>
          <v-btn @click="closeCardDialog">Закрыть</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </template>
  
  <script>
  export default {
    props: {
      dialogVisible: Boolean,
      selectedCard: Object,
    },
    methods: {
      closeCardDialog() {
        this.$emit('close');
      },
      startSorting() {
        // Логика для начала сортировки
        // Вы можете добавить необходимые действия
      },
      showSortedArrayInfo() {
        // Логика для показа данных сортировки
        // Вы можете добавить необходимые действия
      },
      editArray() {
        // Логика для изменения массива
        // Вы можете добавить необходимые действия
      },
      deleteArray() {
        // Логика для удаления массива
        // Вы можете добавить необходимые действия
      },
    },
  };
  </script>
  