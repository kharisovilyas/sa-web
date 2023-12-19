<template>
  <div class="recycler-view">
    <div v-for="item in items" :key="item.id">
      {{ item.title }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
.recycler-view {
  width: 100%;
  max-height: 300px; /* Adjust the height as needed */
  overflow-y: auto; /* Add a vertical scrollbar when content overflows */
  /* Other styles as needed */
}
</style>
