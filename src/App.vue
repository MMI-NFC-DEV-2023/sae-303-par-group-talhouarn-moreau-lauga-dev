<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router/auto'
import LogInOut from './components/LogInOut.vue';
import HeaderPage from './components/headerPage.vue';
import FooterPage from './components/footerPage.vue';
</script>

<template>
  <header>
    <div class="wrapper">
      <h1 class="text-2xl bg-slate-400">Template Principal (Menu/Footer...)</h1>
      <nav>
       
      </nav>
    </div>
  </header>
  <main>
    <HeaderPage />
    <RouterView v-slot="{ Component }">
    <Suspense>
      <component :is="Component" :key="$route.path" />
    </Suspense>
  </RouterView>
  <FooterPage />
  </main>
</template>