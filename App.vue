<script setup>
import { ref, onMounted } from 'vue'
import { loginStore } from '@/stores/index'
import { RouterView } from 'vue-router'
import DefaultLayout from './layouts/DefaultLayout.vue'

const store = loginStore()
onMounted(() => {
    store.onStart()
})

const icons = ref(
      [
        'mdi-facebook',
        'mdi-twitter',
        'mdi-linkedin',
        'mdi-instagram',
      ]
  ) 
</script>

<template>
<v-app id="app">
  <DefaultLayout>
  </DefaultLayout>
  <v-main>      
    <router-view/> 
    <v-spacer></v-spacer>
    <v-card
      style="background-color: #81D4FA; opacity: 0.30; border-color: transparent!important; color: black;"
      class="ma-8 pa-4 text-center d-flex flex-column"
      rounded="lg"

    >
      <div>
        <v-btn
          v-for="icon in icons"
          :key="icon"
          class="mx-4"
          :icon="icon"
          variant="text"
        ></v-btn>
      </div>
  
      <div class="pt-0">
        Phasellus feugiat arcu sapien, et iaculis ipsum elementum sit amet. Mauris cursus commodo interdum. Praesent ut risus eget metus luctus accumsan id ultrices nunc. Sed at orci sed massa consectetur dignissim a sit amet dui. Duis commodo vitae velit et faucibus. Morbi vehicula lacinia malesuada. Nulla placerat augue vel ipsum ultrices, cursus iaculis dui sollicitudin. Vestibulum eu ipsum vel diam elementum tempor vel ut orci. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
      </div>
  
      <v-divider></v-divider>
  
      <div>
        {{ new Date().getFullYear() }} — <strong>Vuetify</strong>
      </div>
    </v-card> 
  </v-main>
</v-app>    
</template>
