<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router/auto'
import LogInOut from './components/LogInOut.vue';
import HeaderPage from './components/headerPage.vue';
import FooterPage from './components/footerPage.vue';
</script>

<template>
 <div class="bg-orange-50">
  <main>
    <HeaderPage />
    <RouterView v-slot="{ Component }">
    <Suspense>
      <component :is="Component" :key="$route.path" />
    </Suspense>
  </RouterView>
  <FooterPage />
  </main>
  </div>
</template>