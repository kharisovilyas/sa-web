<template>
  <v-container fluid fill-height>
    <v-row no-gutters>
      <v-col cols="6">
        <v-row no-gutters class="flex-column" style="height: 100%;">
          <v-col cols="12" style="height: 100%;">
            <v-label>Мои массивы</v-label>
            <floating-button @open-dialog="openDialog" />
            <card-view :items="unsortedItems" />
          </v-col>
        </v-row>
      </v-col>
    </v-row>

    <!-- ArrayDialog component -->
    <array-dialog ref="arrayDialogRef" @submit-array="submitArray" />
  </v-container>
</template>

<script>
import axios from 'axios';

import FloatingButton from '~/components/FloatingButton.vue';
import CardView from '~/components/CardView.vue';
import ArrayDialog from '~/components/ArrayDialog.vue';
import SortedCardView from '~/components/SortedCardView.vue'; // Import the new component

export default {
  components: {
    FloatingButton,
    CardView,
    ArrayDialog,
    SortedCardView, // Add the new component to the components option
  },
  data() {
    return {
      unsortedItems: [],
      sortedItems: [],
    };
  },
  methods: {
    openDialog() {
      this.$refs.arrayDialogRef.openDialog();
    },
    submitArray(newArray) {
      this.sortedItems = [...this.sortedItems, newArray];
      this.unsortedItems = [...this.unsortedItems, newArray];
    },
    async fetchData() {
      try {
        // Fetch unsorted items
        const unsortedResponse = await axios.get('http://localhost:8080/api/v1/load-array/get/all');
        this.unsortedItems = unsortedResponse.data;
      } catch (error) {
        console.error('Ошибка при получении данных:', error);
      }
    },
  },
  mounted() {
    this.fetchData();
  },
};
</script>

<style scoped>
/* Добавьте стили, если необходимо */
</style>
