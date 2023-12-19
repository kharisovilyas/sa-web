<template>
  <div>
    <v-btn @click="openDialog">Добавить массив</v-btn>
    <v-dialog v-model="dialogVisible" max-width="600">
      <v-card>
        <v-card-title>Ввод данных массива</v-card-title>
        <v-card-text>
          <v-form @submit.prevent="saveArray">
            <v-text-field v-model="arrayName" label="Название массива"></v-text-field>
            <v-text-field v-model="arrayData" label="Данные массива (через запятую)"></v-text-field>
            <v-checkbox v-model="sortArray" label="Сортировать массив"></v-checkbox>
            <v-btn type="submit">Сохранить</v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      dialogVisible: false,
      arrayName: "",
      arrayData: "",
      sortArray: false
    };
  },
  methods: {
    openDialog() {
      this.dialogVisible = true;
    },
    async saveArray() {
      const newArray = {
        arrayName: this.arrayName,
        arrayData: this.arrayData.split(",").map(Number)
      };

      try {
        const url = this.sortArray ? 'http://localhost:8080/api/v1/load-array/add' : 'http://localhost:8080/api/v1/load-array/add/without';
        // Отправляем POST запрос
        await axios.post(url, newArray);

        // Закрыть диалоговое окно
        this.dialogVisible = false;
      } catch (error) {
        console.error('Ошибка при отправке данных:', error);
      }
    }
  }
};
</script>
