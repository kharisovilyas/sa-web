<template>
    <v-container fluid>
      <v-stepper v-model="currentStep" alt-labels>
        <v-stepper-header>
          <v-stepper-step :complete="isStepComplete(1)" step="1">Тест 1</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(2)" step="2">Тест 2</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(3)" step="3">Тест 3</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(4)" step="4">Тест 4</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(5)" step="5">Тест 5</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(6)" step="6">Тест 6</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(7)" step="7">Тест 7</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(8)" step="8">Тест 8</v-stepper-step>
          <v-divider></v-divider>
          <v-stepper-step :complete="isStepComplete(9)" step="9">Тест 9</v-stepper-step>
        </v-stepper-header>
  
        <v-stepper-items>
          <v-stepper-content step="1">
            <v-card>
              <v-card-title>Тест добавления 100 массивов</v-card-title>
              <v-card-text>Добавление 100 массивов в базу данных</v-card-text>
              <v-btn @click="runTest(1)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="2">
            <v-card>
              <v-card-title>Тест добавления 1000 массивов</v-card-title>
              <v-card-text>Добавление 1000 массивов в базу данных</v-card-text>
              <v-btn @click="runTest(2)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="3">
            <v-card>
              <v-card-title>Тест добавления 10000 массивов</v-card-title>
              <v-card-text>Добавление 10000 массивов в базу данных</v-card-text>
              <v-btn @click="runTest(3)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="4">
            <v-card>
              <v-card-title>Тест сортировки 100 массивов</v-card-title>
              <v-card-text>Загрузка и сортировка 100 массивов из базы данных</v-card-text>
              <v-btn @click="runTest(4)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="5">
            <v-card>
              <v-card-title>Тест сортировки 1000 массивов</v-card-title>
              <v-card-text>Загрузка и сортировка 1000 массивов из базы данных</v-card-text>
              <v-btn @click="runTest(5)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="6">
            <v-card>
              <v-card-title>Тест сортировки 10000 массивов</v-card-title>
              <v-card-text>Загрузка и сортировка 10000 массивов из базы данных</v-card-text>
              <v-btn @click="runTest(6)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="7">
            <v-card>
              <v-card-title>Тест удаления 100 массивов</v-card-title>
              <v-card-text>Удаление 100 массивов из базы данных</v-card-text>
              <v-btn @click="runTest(7)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="8">
            <v-card>
              <v-card-title>Тест удаления 1000 массивов</v-card-title>
              <v-card-text>Удаление 1000 массивов из базы данных</v-card-text>
              <v-btn @click="runTest(8)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
  
          <v-stepper-content step="9">
            <v-card>
              <v-card-title>Тест удаления 10000 массивов</v-card-title>
              <v-card-text>Удаление 10000 массивов из базы данных</v-card-text>
              <v-btn @click="runTest(9)">Запустить тест</v-btn>
            </v-card>
          </v-stepper-content>
        </v-stepper-items>
      </v-stepper>
    </v-container>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        currentStep: 1,
        tests: [
          { id: 1, title: 'Тест добавления 100 массивов', description: 'Добавление 100 массивов в базу данных' },
          { id: 2, title: 'Тест добавления 1000 массивов', description: 'Добавление 1000 массивов в базу данных' },
          { id: 3, title: 'Тест добавления 10000 массивов', description: 'Добавление 10000 массивов в базу данных' },
          { id: 4, title: 'Тест сортировки 100 массивов', description: 'Загрузка и сортировка 100 массивов из базы данных' },
          { id: 5, title: 'Тест сортировки 1000 массивов', description: 'Загрузка и сортировка 1000 массивов из базы данных' },
          { id: 6, title: 'Тест сортировки 10000 массивов', description: 'Загрузка и сортировка 10000 массивов из базы данных' },
          { id: 7, title: 'Тест удаления 100 массивов', description: 'Удаление 100 массивов из базы данных' },
          { id: 8, title: 'Тест удаления 1000 массивов', description: 'Удаление 1000 массивов из базы данных' },
          { id: 9, title: 'Тест удаления 10000 массивов', description: 'Удаление 10000 массивов из базы данных' },
        ],
      };
    },
    methods: {
      async runTest(testId) {
        try {
          const response = await axios.get(`http://localhost:8080/api/v1/database-tests${this.getTestEndpoint(testId)}`);
          console.log('Результат теста:', response.data);
  
          // Обработка результата теста
          this.tests[testId - 1].isCompleted = true;
          this.currentStep += 1;
  
          // Проверка, можно ли перейти на другую вкладку
          if (this.currentStep > this.tests.length) {
            // Все тесты завершены, перейти на другую вкладку (ваш код)
          }
        } catch (error) {
          console.error('Ошибка при выполнении теста:', error);
        }
      },
      isStepComplete(step) {
        return this.currentStep > step;
      },
      getTestEndpoint(testId) {
        // Возвращает соответствующий эндпоинт для теста
        return [
          '/add-100-arrays',
          '/add-1000-arrays',
          '/add-10000-arrays',
          '/sort-100-arrays',
          '/sort-1000-arrays',
          '/sort-10000-arrays',
          '/clear-database-100-arrays',
          '/clear-database-1000-arrays',
          '/clear-database-10000-arrays',
        ][testId - 1];
      },
    },
  };
  </script>
  
  <style scoped>
  .test-card {
    cursor: pointer;
    margin-bottom: 16px;
  }
  </style>
  