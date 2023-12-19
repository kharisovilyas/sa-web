<!-- Основной компонент -->
<template>
  <v-container fluid fill-height>
    <v-row no-gutters class="flex-column">
      <v-col v-for="item in items" :key="item.id">
        <v-card
          :class="{ 'custom-card-sorted': item.statusOfSorted }"
          @click="openCardDialog(item)"
          @mouseover="hoverCard(true, item.id)"
          @mouseleave="hoverCard(false, item.id)"
          ref="customCard"
        >
          <v-card-title>{{ item.sortedArrayName }}</v-card-title>
          <v-card-text>
            <div>Date of Sorting: {{ item.dateOfSorted }}</div>
            <div>Status: {{ item.statusOfSorted ? 'Sorted' : 'Not Sorted' }}</div>
            <!-- Другие поля из item могут быть добавлены здесь -->
          </v-card-text>
        </v-card>
      </v-col>

      <!-- Импорт компонента CardDialog -->
      <card-dialog
        :dialogVisible="dialogVisible"
        :selectedCard="selectedCard"
        @close="closeCardDialog"
      />
    </v-row>
  </v-container>
</template>

<script>
import CardDialog from '@/components/CardDialog.vue'; // Импорт компонента

export default {
  components: {
    CardDialog
  },
  props: {
    items: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      dialogVisible: false,
      selectedCard: {}
    };
  },
  methods: {
    hoverCard(isHovered, itemId) {
      const card = this.$refs['customCard' + itemId];
      if (card) {
        card.style.boxShadow = isHovered ? '0px 0px 10px 0px rgba(0, 0, 0, 0.5)' : 'none';
      }
    },
    openCardDialog(card) {
      this.selectedCard = card;
      this.dialogVisible = true;
    },
    closeCardDialog() {
      this.dialogVisible = false;
    }
  }
};
</script>

<style scoped>
/* Устанавливаем отступы между карточками */
.custom-card {
  margin-bottom: 16px;
  transition: box-shadow 0.3s ease; /* Плавный переход эффекта тени при наведении */
  
}

/* Добавляем стили для подсветки сортированных карточек */
.custom-card-sorted {
  background-color: #1e3826; /* Зеленый цвет */
  color: #fff; /* Белый цвет для текста */
  margin-bottom: 16px;
  transition: box-shadow 0.3s ease; /* Плавный переход эффекта тени при наведении */
}
</style>
