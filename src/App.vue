<template>
  <v-app id="inspire">
  <!-- Navigation title -->
    <v-navigation-drawer v-model="drawer" app>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title"> . </v-list-item-title>
          <v-list-item-subtitle> yasna team </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>
  <!-- Navigation items -->
      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>   <!-- Use For to manage list items easier -->
          <v-list-item-icon>
            <v-icon color="primary">{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

  <!--Access to different views-->
    <v-app-bar app>
      <v-app-bar-nav-icon
        @click="drawer = !drawer"
        color="primary"
      ></v-app-bar-nav-icon>

      <v-toolbar-title>Multiple Counter</v-toolbar-title>
    </v-app-bar>

    <v-main  class="primary lighten-2 top-gradient">
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    drawer: null,
    //item definition
    items: [
      { title: "Counter", icon: "mdi-calculator", to: "/" },
      { title: "About Project", icon: "mdi-help-box", to: "/about" },
    ],
  }),
};
</script>