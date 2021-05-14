<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
      <v-list-item class="py-2">
        <v-list-item-content>
          <v-list-item-title class="d-flex align-center">
            <v-icon>mdi-arrow-left</v-icon
            ><NuxtLink to="/profile"> Back </NuxtLink>
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>

      <v-divider></v-divider>

      <v-list dense nav>
        <v-list-item v-for="item in items" :key="item.title" link>
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      outlined
      elevation="0"
      color="#fff"
      :clipped-left="clipped"
      fixed
      app
    >
      <v-toolbar-title class="font-weight-bold headline"
        >Profile Settings</v-toolbar-title
      >

      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main>
      <nuxt />
    </v-main>
    <v-footer :absolute="!fixed" app>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  middleware: ['auth'],
  data() {
    return {
      clipped: false,
      drawer: true,
      fixed: true,
      items: [
        { title: 'Profile', icon: 'mdi-view-dashboard' },
        { title: 'Notifications', icon: 'mdi-image' },
      ],
      miniVariant: false,
      right: true,
      title: 'Diploma',
    }
  },
}
</script>

<style>
* {
  font-family: 'Rubik', sans-serif;
}

.v-input--selection-controls .v-input__control {
  width: 100%;
}
.v-tab {
  color: #353232;
}
.v-application .primary--text {
  color: #353232 !important;
  caret-color: #353232 !important;
}

img {
  object-fit: cover;
}
</style>
