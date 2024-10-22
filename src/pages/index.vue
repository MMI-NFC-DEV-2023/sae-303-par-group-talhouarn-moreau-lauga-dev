<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import * as Plot from '@observablehq/plot';
import PlotFigure from "@/components/PlotFigure.js";
import { RouterLink, RouterView } from 'vue-router/auto'
import departements from '@/assets/departements.geojson.json'
import climateData from 'src/assets/climateData3.json'
import filteredTMax from '@/assets/filteredTMax.json'

import { computed } from 'vue';

const options = computed(() => ({
  title: "Les températures maximales des départements en 2024",
  subtitle: "Les moyennes des températures maximales de chaque départements pour l'année 2024",
  projection: {
    type: "mercator",
    domain: departements
  },
  color: {
    type: "quantile",
    n: 5, // Réduit le nombre de valeurs dans la légende
    scheme: "Oranges",
    label: "Moyenne TMax (°C)",
    transform: (d: any) => d,
    legend: true
  },
  marks: [
    Plot.geo(departements, {
      fill: d => {
        const deptName = d.properties.nom;
        const tempData = filteredTMax.find(t => t.Département === deptName);
        return tempData ? tempData.moyenneTMax : 0; // Retourner la valeur moyenneTMax ou 0 si pas de données
      },
      stroke: "#ff8000",
      title: d => {
        const deptName = d.properties.nom;
        const tempData = filteredTMax.find(t => t.Département === deptName);
        return `${deptName} : ${tempData ? tempData.moyenneTMax : "N/A"} °C`; // Afficher moyenneTMax ou "N/A"
      },
      tip: true
    })
  ]
}));
</script>

<template>
  <div class="relative">
    <img
      class="w-full opacity-60"
      src="/public/img/pxclimateaction-4684217_1280.jpg"
      alt="changement climatique"
    />
    <h1
      class="absolute inset-0 flex items-center justify-center text-center text-4xl font-bold text-black"
    >
      Le changement climatique
    </h1>
  </div>
  <div class="p-7 lg:px-36">
    <p>
      Le changement climatique fait référence aux variations des conditions climatiques de la Terre,
      principalement causées par les activités humaines qui augmentent les gaz à effet de serre dans
      l'atmosphère. Ce phénomène entraîne des conséquences majeures, telles que la sécheresse, les
      innondations. 
    </p>
    <p class="mt-4">
      Comprendre ces changements est essentiel pour agir et protéger notre planète. À
      travers nos graphiques, nous explorerons l'évolution des températures et d'autres indicateurs
      clés liés au changement climatique.
    </p>
  </div>
  <div class="p-7 lg:px-36">
    <h2 class="text-2xl font-semibold mt-8">Les températures maximales des départements en 2024</h2>
    <h3 class="text-xl font-medium mt-2">Les moyennes des températures maximales de chaque départements pour l'année 2024</h3>
  </div>
  <div>
    <div class="p-7 lg:px-36">
      <p>
        Pour débuter notre analyse, nous allons examiner un graphique qui présente une carte de la France, découpée par départements, et illustrant la moyenne des températures maximales enregistrées en 2024. Cette représentation visuelle nous permettra d’identifier les départements les plus affectés par la hausse des températures.
      </p>
      <p class="mt-4">
        Les températures maximales jouent un rôle crucial dans l'analyse du changement climatique, car elles sont directement influencées par l'augmentation des gaz à effet de serre dans l'atmosphère. Une hausse prolongée des températures peut accentuer des phénomènes extrêmes tels que les vagues de chaleur, perturbant les écosystèmes, l'agriculture, et la santé humaine. Mais aussi des épisodes de sécheresse, et des risques d'incendi.
      </p>
    </div>
    <div class="lg:w-1/2 flex justify-center">
      <PlotFigure
        class="mt-8 lg:mt-0"
        :options="options"
        :keys="options"
      />
    </div>
  </div>
  <div class="p-7 lg:px-36 lg:w-1/2 lg:ml-auto">
    <p>
      Les températures maximales moyennes enregistrées en 2024 montrent des variations importantes entre les départements français, allant de 14,67°C (Manche) à 23,08°C (Vaucluse). On peut identifier certaines tendances géographiques et climatologiques intéressantes à partir de ces données.
    </p>
    <ul class="mt-4">
      <li>Nord et Nord-Ouest : Les départements du nord et du nord-ouest, tels que la Manche (14,67°C) et le Pas-de-Calais (15,6°C), présentent des températures moyennes plus basses, ce qui peut s'expliquer par l'influence océanique et la latitude plus élevée.</li>
      <li>Centre et Ouest : Des départements comme le Maine-et-Loire (18,49°C) et la Vienne (18,89°C) ont des températures légèrement plus modérées, reflétant un climat tempéré mais avec une influence continentale plus marquée.</li>
      <li>Inégalités régionales face à la chaleur : Les écarts de température entre le sud (Vaucluse à 23,08°C) et le nord (Manche à 14,67°C) pourraient accentuer les disparités dans la gestion des ressources hydriques et l'adaptation des infrastructures face aux épisodes de chaleur extrême.</li>
      <li>Effets possibles sur l'agriculture et l'économie : Des départements fortement agricoles, comme la Drôme (21,29°C) et le Lot-et-Garonne (20,92°C), pourraient être particulièrement vulnérables à l'augmentation des températures, ce qui affecterait les cultures sensibles à la chaleur (comme le blé, le vin, ou les fruits).</li>
    </ul>
  </div>
</template>