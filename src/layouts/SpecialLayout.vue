<template>
  <q-layout view="hHh lpR fFf">

    <q-header class="bg-primary text-white" height-hint="98">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="https://cdn.quasar.dev/logo-v2/svg/logo-mono-white.svg">
          </q-avatar>
          Visualisierung von Lösungsalgorithmen
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs class="bg-primary text-white" align="left">
        <q-route-tab to="/" label="Classic" />
        <q-route-tab to="/Special" label="Special" />          
      </q-tabs>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script lang="ts">



import { defineComponent } from 'vue'

export default defineComponent({
  name: 'MainLayout',

  components: {
    
  },

  setup () {

    return {
      
    }
  }
})
</script>

<style lang="scss" scoped>
.q-toolbar{
  box-shadow: 3px 3px 10px grey;
}
</style>
