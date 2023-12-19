<template>
    <v-dialog v-model="dialogVisible" :top="0">
      <v-card v-if="selectedCard">
        <!-- Остальной код остается неизменным -->
  
        <v-card-actions>
          <!-- Остальные кнопки остаются без изменений -->
          <v-btn @click="startSorting">Остортировать массив</v-btn>
          <v-btn @click="deleteArray">Удалить массив</v-btn>
          <v-btn @click="closeCardDialog">Закрыть</v-btn>
        </v-card-actions>
  
        <!-- Используем встроенный компонент transition для эффекта плавного появления/исчезновения диалога -->
        <transition name="fade">
          <!-- Показываем ArraySortingInfo в новом диалоге -->
          <v-dialog v-if="showArraySortingInfo" @input="closeArraySortingInfoDialog" :top="0">
            <array-sorting-info :sortedArray="sortedArray" />
            <v-btn @click="closeArraySortingInfoDialog">Закрыть информацию о сортировке</v-btn>
          </v-dialog>
        </transition>
      </v-card>
    </v-dialog>
  </template>
  
  
  <script>
  import axios from 'axios';
  import ArraySortingInfo from '@/components/ArraySortingInfo.vue';
  
  export default {
    props: {
      dialogVisible: Boolean,
      selectedCard: Object,
    },
    data() {
      return {
        showArraySortingInfoDialog: false,
        sortedArray: null,
      };
    },
    methods: {
      closeArraySortingInfoDialog() {
        this.showArraySortingInfoDialog = false;
      },
      async showSortedArrayInfo() {
        try {
          // Проверяем, что у нас есть selectedCard и в нем есть arrayId
          if (this.selectedCard && this.selectedCard.arrayId) {
            const arrayId = this.selectedCard.arrayId;
            // Выполняем GET-запрос к API, чтобы получить информацию о сортировке
            const response = await axios.get(`http://localhost:8080/api/v1/sorted-array/get/once?arrayId=${arrayId}`);
            this.sortedArray = response.data;
  
            // Показываем информацию о сортировке
            this.showArraySortingInfoDialog = true;
          } else {
            console.error('Ошибка: selectedCard или arrayId отсутствует');
          }
        } catch (error) {
          // Обрабатываем ошибку
          console.error('Ошибка при получении информации о сортировке:', error);
        }
      },
  
      // Остальные методы остаются без изменений
    },
  };
  </script>
  