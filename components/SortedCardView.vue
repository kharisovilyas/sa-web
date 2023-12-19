<template>
    <v-container fluid fill-height>
      <v-row no-gutters class="flex-column">
        <v-col v-for="sortedItem in sortedItems" :key="sortedItem.sortedArrayId">
          <v-card>
            <v-card-title class="center-text">{{ sortedItem.sortedArrayName }}</v-card-title>
            <v-card-text>
              <div>Date of Sorted: {{ formatDateTime(sortedItem.dateOfSorted) }}</div>
              <div>Time of Implementation: {{ sortedItem.timeOfImpl }}</div>
              <div>Status of Sorted: {{ sortedItem.statusOfSorted ? 'Sorted' : 'Not Sorted' }}</div>
              <div v-if="sortedItem.array_data">Array Data: {{ sortedItem.array_data.join(', ') }}</div>
              <div v-else>No Array Data</div>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </template>
  
  <script>
  export default {
    props: {
      sortedItems: {
        type: Array,
        required: true
      }
    },
    methods: {
      formatDateTime(dateTime) {
        return new Date(dateTime);
      }
    }
  };
  </script>
  
  <style scoped>
  .v-card {
    margin-bottom: 5%;
  }
  
  </style>
  