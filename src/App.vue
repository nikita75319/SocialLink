<template>
  <v-app id="app">
    <v-navigation-drawer
      color="green"
      dark
      absolute
      permanent
      right
      hide-overlay
      expand-on-hover
    >
      <v-list-item two-line class="px-2">
        <v-list-item-avatar>
          <img src="https://randomuser.me/api/portraits/men/2.jpg" />
        </v-list-item-avatar>

        <v-list-item-content class="px-2">
          <v-list-item-title>Ervin Howell</v-list-item-title>
          <v-list-item-subtitle>Logged In</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider class="my-3"></v-divider>

      <v-list shaped nav dense>
        <v-list-item link to="/">
          <v-list-item-icon>
            <v-icon>mdi-home</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Главная</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link to="/profile/2">
          <v-list-item-icon>
            <v-icon>mdi-account</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Мой профиль</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-list-item link to="/about">
          <v-list-item-icon>
            <v-icon>mdi-account-multiple-plus</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Найти друзей</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-main class="px-12 py-3">
      <v-container fluid>
        <router-view />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    //
  }),
};
</script>
