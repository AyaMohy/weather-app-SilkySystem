<template>
  <q-page class="flex flex-center">
    <app-header />
    <weather-data/>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import appHeader from "src/components/app-header.vue";
import weatherData from "src/components/weather-data.vue";
export default defineComponent({
  name: "IndexPage",
  components: { appHeader, weatherData },
});
</script>
