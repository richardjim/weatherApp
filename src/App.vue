<template>
  <div class="flex flex-col min-h-screen font-Roboto bg-weather-primary">
    <RouterView />
    <SiteNavigation />

  </div>
</template>

<script>
import { RouterView } from 'vue-router'
import SiteNavigation from './components/SiteNavigation.vue';
export default {
  components: { SiteNavigation }
}
</script>