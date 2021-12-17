<template>
  <v-app class="pb-5">
    <v-app-bar app color="primary" dark>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
    </v-app-bar>
    <v-navigation-drawer v-model="drawer" absolute temporary>
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item
            :to="{
              name: 'Client',
            }"
          >
            <v-list-item-title> Clientes </v-list-item-title>
          </v-list-item>
          <v-list-item
            :to="{
              name: 'Products',
            }"
          >
            <v-list-item-title> Productos </v-list-item-title>
          </v-list-item>

          
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <v-main class="pb-6">
      <router-view />
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data: () => ({
    drawer: false,
    group: null,
  }),
  watch: {
    group() {
      this.drawer = false;
    },
  },
};
</script>
