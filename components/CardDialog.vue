<!-- CardDialog.vue -->
<template>
    <v-dialog v-model="dialogVisible" @input="fetchSortedArrayData">
      <v-card v-if="selectedCard">
        <!-- Исходный массив -->
        <v-card-title>Исходный {{ selectedCard.arrayName }}</v-card-title>
        <v-card-text>
          <div>Дата загрузки: {{ selectedCard.dateOfLoad }}</div>
          <div>Статус загрузки: {{ selectedCard.statusOfLoad ? 'Загружен' : 'Не загружен' }}</div>
          <div>Статус сортировки: {{ selectedCard.statusOfSorted ? 'Отсортирован' : 'Не отсортирован' }}</div>
          <div v-if="selectedCard.arrayData">Данные массива: {{ selectedCard.arrayData.join(', ') }}</div>
        </v-card-text>
  
        <!-- Кнопки действий -->
        <v-card-actions>
          <v-btn @click="startSorting">Остортировать массив</v-btn>
          <v-btn @click="deleteArray">Удалить массив</v-btn>
          <v-btn @click="closeCardDialog">Закрыть</v-btn>
        </v-card-actions>
  
        <!-- Отсортированный массив -->
        <v-card-title v-if="showArraySortingInfo">Отсортированный {{ selectedCard.arrayName }}</v-card-title>
        <v-card-text v-if="showArraySortingInfo">
          <div v-if="sortedArray">
            <div>Идентификатор сортированного массива: {{ sortedArray.sortedArrayId }}</div>
            <div>Название сортированного массива: {{ sortedArray.sortedArrayName }}</div>
            <div>Дата сортировки: {{ sortedArray.dateOfSorted }}</div>
            <div>Время выполнения сортировки: {{ sortedArray.timeOfImpl }}</div>
            <div>Статус сортировки: {{ sortedArray.statusOfSorted ? 'Отсортирован' : 'Не отсортирован' }}</div>
            <div v-if="sortedArray.array_data">Данные массива: {{ sortedArray.array_data.join(', ') }}</div>
            <div v-if="!sortedArray.statusOfSorted">Массив неотсортирован</div>
          </div>
        </v-card-text>
      </v-card>
    </v-dialog>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    props: {
      dialogVisible: Boolean,
      selectedCard: Object,
    },
    data() {
        return {
            showArraySortingInfo: false,
            showArraySortingInfoDialog: false,
            sortedArray: null,
        };
    },
    methods: {
      closeCardDialog() {
        this.$emit('close');
      },

      async startSorting() {
        try {
          if (this.selectedCard && this.selectedCard.arrayId) {
            const arrayId = this.selectedCard.arrayId;
            
            // Выполняем POST-запрос к API
            const response = await axios.post(`http://localhost:8080/api/v1/sorted-array/start/sorting?arrayId=${arrayId}`);
  
            // Обрабатываем успешный ответ (response.data)
            console.log('Массив отсортирован успешно:', response.message);
  
            // Получаем информацию о сортированном массиве
            this.fetchSortedArrayData(arrayId);
          } else {
            console.error('Ошибка: selectedCard или arrayId отсутствует');
          }
        } catch (error) {
          // Обрабатываем ошибку
          console.error('Ошибка при сортировке массива:', error);
        } finally {
          // Закрываем диалог после выполнения запроса (можно изменить логику в соответствии с вашими требованиями)
          
        }
      },
      async fetchSortedArrayData(arrayId) {
        try {
          const response = await axios.post(`http://localhost:8080/api/v1/sorted-array/get/once?arrayId=${arrayId}`);
          this.sortedArray = response.data;
  
          // Показываем информацию о сортированном массиве
          this.showArraySortingInfo = true;
        } catch (error) {
          console.error('Ошибка при получении данных о сортированном массиве:', error);
        }
      },
      async showSortedArrayInfo() {
      try {
        // Проверяем, что у нас есть selectedCard и в нем есть arrayId
        if (this.selectedCard && this.selectedCard.arrayId) {
          const arrayId = this.selectedCard.arrayId;

          // Если statusOfSorted равен true, то получаем данные и отображаем их
          if (this.selectedCard.statusOfSorted) {
            await this.fetchSortedArrayData(arrayId);
            this.showArraySortingInfoDialog = true;
          } else {
            // Если statusOfSorted равен false, то показываем кнопку и отложенно получаем данные
            this.showSortedArrayInfoDialog = true;
          }
        } else {
          console.error('Ошибка: selectedCard или arrayId отсутствует');
        }
      } catch (error) {
        // Обрабатываем ошибку
        console.error('Ошибка при получении информации о сортировке:', error);
      }
    },
      async deleteArray() {
        try {
          // Проверяем, что у нас есть selectedCard и в нем есть arrayId
          if (this.selectedCard && this.selectedCard.arrayId) {
            const sortedArrayId = this.selectedCard.arrayId;
  
            // Выполняем POST-запрос к API
            const response = await axios.post(`http://localhost:8080/api/v1/load-array/delete?arrayId=${sortedArrayId}`);
  
            // Обрабатываем успешный ответ (response.data)
            console.log('Массив успешно удален:', response.data);
  
            // Дополнительные действия, если необходимо
          } else {
            console.error('Ошибка: selectedCard или arrayId отсутствует');
          }
        } catch (error) {
          // Обрабатываем ошибку
          console.error('Ошибка при удалении массива:', error);
  
          // Дополнительные действия при ошибке, если необходимо
        } finally {
          // Закрываем диалог после выполнения запроса (можно изменить логику в соответствии с вашими требованиями)
          this.closeCardDialog();
        }
      },
    },
    watch: {
    dialogVisible(newValue) {
      if (newValue) {
        // Если диалог видим, обновляем данные
        this.fetchSortedArrayData(this.selectedCard.arrayId);
      }
    },
  },
    mounted() {
        // При монтировании компонента тоже вызываем метод для обновления данных
        if (this.dialogVisible) {
        this.fetchSortedArrayData(this.selectedCard.arrayId);
        }
    },
  };
  </script>
  
  
  