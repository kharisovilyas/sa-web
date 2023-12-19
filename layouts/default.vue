<template>
  <v-app dark>
    <v-app-bar app>
      <v-app-bar-title>Sorting Algorithms</v-app-bar-title>
      <v-spacer></v-spacer>
      <v-tabs v-model="tab" grow>
        <v-spacer></v-spacer>
        <v-tab @click="changeTab(0)">Сортировка</v-tab>
        <v-tab @click="changeTab(1)">Тесты базы данных</v-tab>
      </v-tabs>
    </v-app-bar>
    <!-- Удален блок с v-navigation-drawer -->
    <v-main>
      <v-container>
        <!-- Передаем свойство items компоненту Nuxt -->
        <Nuxt :items="items" />
        <v-tab-item v-if="tab === 0">Содержимое вкладки 1</v-tab-item>
        <v-tab-item v-if="tab === 1">Содержимое вкладки 2</v-tab-item>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      tab: 0, // Выбранная вкладка
    };
  },
  methods: {
    changeTab(index) {
      this.tab = index;
      if (index === 0) {
        this.$router.push('/'); // Перейти на страницу "/"
      }
      if (index === 1) {
        this.$router.push('/tests'); // Перейти на страницу "second"
      }
    },
  },
};
</script>
