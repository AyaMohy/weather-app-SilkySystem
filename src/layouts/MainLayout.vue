<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>


        <q-toolbar-title>
          Weather App
        </q-toolbar-title>
      </q-toolbar>
    </q-header>



    <q-page-container>
      <router-view />
    </q-page-container>

     <q-footer elevated class=" text-white">
      <q-toolbar>
        <q-toolbar-title>
          <!-- <div>Silky Systems</div> -->
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'



export default defineComponent({
  name: 'MainLayout',

  components: {
    // EssentialLink
  },

  setup () {
    const leftDrawerOpen = ref(false)

    return {

    }
  }
})
</script>
