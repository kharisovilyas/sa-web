<template>
  <v-app dark>
    <v-app-bar app>
      <v-toolbar-title>Sorting Algorithms</v-toolbar-title>
    </v-app-bar>
    <!-- Удален блок с v-navigation-drawer -->
    <v-main>
      <v-container>
        <!-- Передаем свойство items компоненту Nuxt -->
        <Nuxt :items="items" />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout'
};
</script>
