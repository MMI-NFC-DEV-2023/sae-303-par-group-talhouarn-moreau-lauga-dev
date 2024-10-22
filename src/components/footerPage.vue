<script setup lang="ts">

import { RouterLink } from 'vue-router'
</script>

<template>
  <footer class="pb-10 pt-10 lg:space-y-0 bg-zinc-300">
    <div class="lg:px-50 lg:grid lg:grid-cols-3">
      <nav
        class="px-5 gap-8 space-y-8 lg:columns-3 lg:col-start-1 lg:col-span-1 lg:px-0 *:break-inside-avoid *:space-y-3"
      >
        <div>
          <ul class="flex justify-center  gap-28 text-black font-bold text-base lg:text-base lg:flex-col lg:gap-10 lg:pl-40 underline">
            <li><RouterLink to="/contact">Contact</RouterLink></li>
            <li><RouterLink to="/infos">Infos</RouterLink></li>
            <li><RouterLink to="/:page404(.*)">Billetterie</RouterLink></li>
          </ul>
        </div>
      </nav>
      <div class="lg:col-start-2">
        <div>
          <p class="mt-7 mx-2 text-center lg:justify-center lg:col-span-2">
            Joignez vous à nous pour une expérience immersive qui éveille votre fascination pour
            l'art de l'architecture contemporaine.
          </p>
        </div>
        <div class="flex justify-center mt-5">
          <RouterLink to="/">
          <IconLogo class="h-12 w-12" />
          </RouterLink>
        </div>
      </div>
      <div>
        <p class="text-center mt-3 mx-2">Retrouvez nous sur les Réseaux Sociaux</p>

        <div
          class="px-5 text-black py-8 space-y-6 text-center lg:flex lg:justify-around lg:items-center lg:space-y-0"
        >
        
          <div class="flex gap-12 justify-center">
            
            <RouterLink aria-label="Facebook" to="/">
              <LogoFacebook aria-hidden="true" class="h-12 w-12 mt-4" />
            </RouterLink>
            <RouterLink aria-label="Instagram" to="/">
              <LogoInsta1 aria-hidden="true" class="h-20 w-20" />
            </RouterLink>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>
