<!-- eslint-disable vue/multi-word-component-names -->
<script setup lang="ts">
import * as Plot from '@observablehq/plot'
import PlotFigure from '@/components/PlotFigure.js'
import { RouterLink, RouterView } from 'vue-router/auto'
import departements from '@/assets/departements.geojson.json'
import climateData from 'src/assets/climateData3.json'
import filteredTMax from '@/assets/filteredTMax.json'

import { computed } from 'vue'

const options = computed(() => ({
  title: 'Les températures maximales des départements en 2024',
  subtitle: "Les moyennes des températures maximales de chaque départements pour l'année 2024",
  projection: {
    type: 'mercator',
    domain: departements
  },
  color: {
    type: 'quantile',
    n: 5, // Réduit le nombre de valeurs dans la légende
    scheme: 'Oranges',
    label: 'Moyenne TMax (°C)',
    transform: (d: any) => d,
    legend: true
  },
  marks: [
    Plot.geo(departements, {
      fill: (d) => {
        const deptName = d.properties.nom
        const tempData = filteredTMax.find((t) => t.Département === deptName)
        return tempData ? tempData.moyenneTMax : 0 // Retourner la valeur moyenneTMax ou 0 si pas de données
      },
      stroke: '#ff8000',
      title: (d) => {
        const deptName = d.properties.nom
        const tempData = filteredTMax.find((t) => t.Département === deptName)
        return `${deptName} : ${tempData ? tempData.moyenneTMax : 'N/A'} °C` // Afficher moyenneTMax ou "N/A"
      },
      tip: true
    })
  ]
}))
</script>

<template>
  <div class="relative">
    <img
      class="w-full opacity-90"
      src="/public/img/landscape-cracked-earth-from-drought.jpg"
      alt="changement climatique"
    />
    <h1
      class="absolute inset-0 flex items-center justify-center text-center font-bold text-black lg:text-7xl"
    >
      Le changement climatique
    </h1>
  </div>

  <div class="p-7 lg:px-36">
    <p>
      Le changement climatique fait référence aux variations des conditions climatiques de la Terre,
      principalement causées par les activités humaines qui augmentent les gaz à effet de serre dans
      l'atmosphère. Ce phénomène entraîne des conséquences majeures, telles que la sécheresse, les
      inondations.
    </p>
    <p class="mt-4">
      Comprendre ces changements est essentiel pour agir et protéger notre planète. À travers nos
      graphiques, nous explorerons l'évolution des températures et d'autres indicateurs clés liés au
      changement climatique.
    </p>
    <h2 class="mt-6 font-bold">
      Le climat se réchauffe : aperçu des départements les plus affectés
    </h2>

    <p class="mt-4">
      Pour débuter notre analyse, nous allons examiner un graphique qui présente une carte de la
      France, découpée par départements, et illustrant la moyenne des températures maximales
      enregistrées en 2024. Cette représentation visuelle nous permettra d’identifier les
      départements les plus affectés par la hausse des températures.
    </p>
    <p class="mt-4">
      Les températures maximales jouent un rôle crucial dans l'analyse du changement climatique, car
      elles sont directement influencées par l'augmentation des gaz à effet de serre dans
      l'atmosphère. Une hausse prolongée des températures peut accentuer des phénomènes extrêmes
      tels que les vagues de chaleur, perturbant les écosystèmes, l'agriculture, et la santé
      humaine. Mais aussi des épisodes de sécheresse, et des risques d'incendie.
    </p>
  </div>

  <div class="p-7 lg:flex lg:space-x-8 lg:px-36">
    <div class="flex justify-center lg:w-1/2">
      <PlotFigure class="mt-8 lg:mt-0" :options="options" :keys="options" />
    </div>

    <!-- Texte explicatif, aligné à la hauteur de la carte en version desktop -->
    <div class="flex items-center lg:ml-auto lg:w-1/2 lg:items-start">
      <div>
        <p class="mb-4">
          Ce graphique représente la moyenne des températures maximales enregistrées dans les
          départements français pour l'année 2024
        </p>
        <h4>1. Tendance générale</h4>
        <ul class="mt-4 list-inside list-disc">
          <li class="mb-4">
            La palette de couleurs, allant du jaune pâle à l'orange foncé, indique les variations de la température maximale moyenne entre les départements. Plus la teinte est foncée, plus la température maximale moyenne est élevée.
          </li>
          <li class="mb-4">
            On observe une tendance générale où les départements situés dans le sud de la France, comme ceux de la région Provence-Alpes-Côte d'Azur, montrent des températures maximales plus élevées, atteignant des moyennes supérieures à 20°C.
          </li>
        </ul>
        <h4>2. Différences régionales</h4>
        <ul class="mt-4 list-inside list-disc">
          <li class="mb-4">
            Nord et Nord-Ouest : Les départements du nord de la France, comme la Seine-Saint-Denis, ont des températures maximales moyennes plus basses, autour de 17,58°C, ce qui est cohérent avec la latitude plus élevée et l'influence océanique. Cela se traduit par des couleurs plus claires dans le nord du pays.
          </li>
          <li class="mb-4">
            Centre et Sud : Les départements du centre et du sud de la France, comme ceux du Massif Central et du sud-ouest, sont les plus touchés par des températures maximales plus élevées, dépassant souvent les 18°C et atteignant 20°C dans certaines régions. Ces zones sont représentées par des couleurs plus foncées.
          </li>
        </ul>
        <h4 class="mb-3">3. Disparités de température</h4>
        <p class="mb-4">Les écarts entre les températures du nord et du sud sont significatifs. Par exemple, en Seine-Saint-Denis, la température maximale moyenne est de 17,58°C, alors que dans des départements du sud, la moyenne dépasse 20°C. Ces écarts peuvent refléter des différences dans l'exposition aux phénomènes climatiques extrêmes, comme les vagues de chaleur.</p>
        <h4 class="mb-3">4. Impact climatique potentiel</h4>
        <p>Ces variations de température maximale pourraient avoir un impact direct sur les infrastructures, la gestion des ressources en eau et l'agriculture, surtout dans les régions du sud, où les températures sont plus élevées. Les départements affichant des températures maximales élevées, notamment dans le sud, pourraient connaître des périodes de chaleur prolongées, aggravant les risques de sécheresse.</p>
        En résumé, ce graphique illustre la répartition géographique des températures maximales en France pour 2024, soulignant un contraste notable entre les départements du nord, qui restent relativement frais, et ceux du sud, qui subissent des températures maximales plus élevées.
      </div>
    </div>
  </div>
</template>
