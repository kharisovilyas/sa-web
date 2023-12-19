<template>
  <v-dialog v-model="dialogVisible" max-width="600px" lazy>
    <!-- Your existing code remains unchanged -->
  </v-dialog>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      dialogVisible: false,
      newArrayName: '',
      newArraySize: '',
      newArrayData: '',
      currentStep: 1,
    };
  },
  methods: {
    // Your existing methods remain unchanged
  },
};
</script>

<style scoped>
/* Your existing styles remain unchanged */
</style>
