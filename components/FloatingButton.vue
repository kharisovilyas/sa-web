<template>
  <v-btn icon class="white--text" @click="openDialog">
    <v-icon>mdi-plus</v-icon>
  </v-btn>
</template>

<script>
export default {
  methods: {
    openDialog() {
      // Открываем диалоговое окно
      this.$emit('open-dialog');
    }
  }
};
</script>
