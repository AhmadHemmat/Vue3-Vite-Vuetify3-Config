<template>
<v-app-bar
      dir="rtl"
      color="light-blue-lighten-5"
      rounded="lg"
      elevation="12"
      app
    >
        <v-btn to="/" icon="mdi-home-circle" size="large"></v-btn>
        <v-btn v-if="store.isAuthenticated" to="/dashboard" icon="mdi-account-circle" size="large"></v-btn>
        <!-- <v-btn to="" icon="mdi-map-marker" size="large"></v-btn> -->
        <!-- <v-btn to="" icon="mdi-magnify" size="large"></v-btn> -->
        <!-- <v-spacer></v-spacer> -->
        <v-spacer></v-spacer>
        <v-btn v-if="!store.isAuthenticated" to="/register" icon="mdi-account-plus" size="large"></v-btn>
        <v-btn v-if="!store.isAuthenticated" to="/login" icon="mdi-login" size="large"></v-btn>
        <v-btn v-if="store.isAuthenticated" to="/login" icon="mdi-logout" size="large" @click="logout"></v-btn>
</v-app-bar>
<v-container v-if="windowWidth < 500">
  <v-bottom-navigation
  :active="active"
  color="indigo"
>
  <v-btn>
    <v-icon v-if="buyBox">mdi-cart</v-icon>
    <v-icon v-if="!buyBox">mdi-cart-off</v-icon>
    سبد خرید
  </v-btn>

  <v-btn>
    <v-icon>mdi-silverware</v-icon>

    سفارش
  </v-btn>

  <v-btn>
    <v-icon>mdi-home-circle</v-icon>
    خانه
  </v-btn>

  <v-btn>
    <v-icon v-if="homeAddress">mdi-home-map-marker</v-icon>
    <v-icon v-if="!homeAddress">mdi-map-marker-off</v-icon>
    آدرس
  </v-btn>
  <v-btn to="/dashboard">
    <v-icon>mdi-account-circle</v-icon>
    پروفایل
  </v-btn>
</v-bottom-navigation>
</v-container>
</template>

<script setup>
  import { ref } from 'vue'
  import { loginStore } from '@/stores/index'

const store = loginStore()


  const active = ref(true)
  // const logo = ref('@/assets/profile.png')
  let windowWidth = ref(window.innerWidth)
  const buyBox = ref(false)
  const homeAddress = ref(false)


  function logout() {
    store.logout()
  }
</script>

<style>

.footer {
  bottom: 0;
  position: sticky;
  height: auto;
}
</style>