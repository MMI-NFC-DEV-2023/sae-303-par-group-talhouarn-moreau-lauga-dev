<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import * as Plot from '@observablehq/plot'
import PlotFigure from '@/components/PlotFigure.js'
import { RouterLink, RouterView } from 'vue-router/auto'
import departements from '@/assets/departements.geojson.json'
import climateData from '@/assets/climateData3.json'
import filteredTMax from '@/assets/filteredTMax.json'
import cleanData from '@/assets/cleanData.json'

import { computed } from 'vue'

const options = computed(() => ({
  title: 'Les températures moyennes maximales des départements en 2024',
  subtitle: 'Les moyennes des températures maximales par departements en 2024',
  projection: {
    type: 'mercator',
    domain: departements
  },
  color: {
    type: 'quantile',
    n: 5, // Réduit le nombre de valeurs dans la légende
    scheme: 'Oranges',
    label: 'Moyenne TMax (°C)',
    transform: (d) => d,
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
      class="opacity-90 brightness-50 filter backdrop-contrast-150"
      src="/public/img/landscape-cracked-earth-from-drought.webp"
      alt="changement climatique"
    />
    <h1
      class="absolute inset-0 flex items-center justify-center px-5 text-center font-bold text-orange-50 lg:text-7xl"
    >
      Le changement climatique en France et dans le lot et garonne
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
      Le climat se réchauffe : aperçu des départements les plus affectés en France
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

  <div class="p-7 lg:px-36">
    <div class="">
      <PlotFigure class="mt-8 lg:mt-0" :options="options" :keys="options" />
      <p class="mb-2 mt-3">Sources</p>
      <a class="underline text-orange-400" href="https://france-geojson.gregoiredavid.fr/"> Source 1</a>
      <a class="underline text-orange-400"
        href="https://explore.data.gouv.fr/fr/datasets/5eb236728ad018f2f0fe1b9e/#/resources/dd0df06a-85f2-4621-8b8b-5a3fe195bcd7"
      >
        Source 2</a
      >
    </div>

    <!-- Texte explicatif, aligné à la hauteur de la carte en version desktop -->
    <div class="mt-8">
      <p class="mb-4">
        Ce graphique représente la moyenne des températures maximales enregistrées dans les
        départements français pour l'année 2024
      </p>
      <ul class="mt-4 list-inside list-disc">
        <li class="mb-4">
          Sud de la France : Les départements du sud, comme les Alpes-Maritimes (22,41°C), la
          Corse-du-Sud (22,94°C), et le Vaucluse (23,08°C), affichent les températures les plus
          élevées. Cela est conforme aux tendances climatiques où les régions méditerranéennes sont
          naturellement plus chaudes.
        </li>
        <li class="mb-4">
          Nord et Nord-Ouest : Les départements du nord et du nord-ouest, tels que la Manche
          (14,67°C) et le Pas-de-Calais (15,6°C), présentent des températures moyennes plus basses,
          ce qui peut s'expliquer par l'influence océanique et la latitude plus élevée.
        </li>
        <li class="mb-4">
          Centre et Ouest : Des départements comme le Maine-et-Loire (18,49°C) et la Vienne
          (18,89°C) ont des températures légèrement plus modérées, reflétant un climat tempéré mais
          avec une influence continentale plus marquée.
        </li>
        <li class="mb-4">
          Inégalités régionales face à la chaleur : Les écarts de température entre le sud (Vaucluse
          à 23,08°C) et le nord (Manche à 14,67°C) pourraient accentuer les disparités dans la
          gestion des ressources hydriques et l'adaptation des infrastructures face aux épisodes de
          chaleur extrême.
        </li>
        <li class="mb-4">
          Effets possibles sur l'agriculture et l'économie : Des départements fortement agricoles,
          comme la Drôme (21,29°C) et le Lot-et-Garonne (20,92°C), pourraient être particulièrement
          vulnérables à l'augmentation des températures, ce qui affecterait les cultures sensibles à
          la chaleur (comme le blé, le vin, ou les fruits).
        </li>
      </ul>

      <p class="mb-3">
        En résumé, ce graphique illustre la répartition géographique des températures maximales en
        France pour 2024, soulignant un contraste notable entre les départements du nord, qui
        restent relativement frais, et ceux du sud, qui subissent des températures maximales plus
        élevées.
      </p>
    </div>

    <section>
      <div class="mt-10 border-t border-t-gray-400 pt-10">
        <h1 class="mb-4 mt-8">Les prévisions</h1>
        <p>
          Les changements climatiques que nous observons aujourd'hui ne sont que le début d'une
          transformation plus profonde et plus durable de notre environnement. Grâce aux données
          réelles et prévisionnelles, il est possible d'anticiper l'évolution des conditions
          météorologiques, notamment la hausse des températures.
        </p>
      </div>
      <div>
        <h2 class="mt-4">Évolution de la température moyenne en France (2005-2050)</h2>
        <h3 class="mb-3">Les températures en degré Celsius prévues jusqu'à 2050</h3>
        <PlotFigure
          :options="{
            marks: [
              Plot.line(cleanData, {
                x: 'Year',
                y: 'Temperature',
                stroke: (d) => d.Type,
                strokeWidth: 2
              }),
              Plot.dot(cleanData, {
                x: 'Year',
                y: 'Temperature',
                fill: (d) => d.Type,
                r: 4,
                tip: (d) => `Année: ${d.Year}\nTempérature: ${d.Temperature.toFixed(2)}°C`
              })
            ],
            x: { label: 'Année' },
            y: { label: 'Température (°C)', grid: true },
            color: {
              domain: ['Données réelles', 'Données prévisionnelles'],
              legend: true,
              range: ['red', 'gold']
            }
          }"
        />
        <p class="mb-2 mt-3">Sources</p>
        <a class="underline text-orange-400" href="https://donneespubliques.meteofrance.fr/"> Données prévisionnelles</a>
        <h3 class="mb-3 mt-4">Interprétation des données</h3>
        <ul class="list-inside list-disc">
          <li class="mb-2">
            Données réelles (en rouge) : De 2005 jusqu'à environ 2025, les points rouges montrent
            l'évolution des températures mesurées. On observe une tendance générale à la hausse,
            malgré quelques fluctuations à la baisse dans certaines années. La température moyenne
            est passée d'environ 12,3°C en 2005 à environ 13,6°C en 2025. C'est une augmentation
            significative en 20 ans.
          </li>
          <li class="mb-2">
            Données prévisionnelles (en jaune) : Après 2025, les points jaunes représentent les
            prévisions de température moyenne jusqu'en 2050. La courbe montre une montée continue
            des températures avec une augmentation progressive qui projette des températures autour
            de 14,8°C à 15°C d'ici 2050. Les prévisions soulignent une tendance haussière sans signe
            de stabilisation.
          </li>
        </ul>
        <h3 class="mb-3">Analyse des tendances</h3>
        <ul class="list-inside list-disc">
          <li class="mb-2">
            Hausse constante des températures : La température moyenne est en constante
            augmentation, ce qui reflète les impacts du changement climatique en France. La hausse
            de température pourrait être due à plusieurs facteurs, tels que l'augmentation des gaz à
            effet de serre et les activités humaines.
          </li>
          <li class="mb-4">
            Différences entre les données réelles et prévisionnelles : Si les données réelles
            montrent des fluctuations d'année en année, les prévisions semblent indiquer une
            croissance plus stable et régulière. Cela peut refléter une modélisation basée sur des
            scénarios climatiques futurs.
          </li>
        </ul>
        <h3 class="mb-3">Implications</h3>
        <ul class="list-inside list-disc">
          <li class="mb-2">
            Changement climatique : Cette augmentation des températures est alarmante car elle peut
            accentuer les phénomènes météorologiques extrêmes, comme les vagues de chaleur, et avoir
            des effets importants sur l'agriculture, la biodiversité et les ressources en eau.
          </li>
          <li class="mb-8">
            Réponse politique et sociale : La courbe montre clairement que des actions sont
            nécessaires pour limiter cette augmentation et ses effets néfastes. Les décideurs
            peuvent utiliser ce genre de données pour planifier des politiques de réduction des
            émissions de CO2 et d’adaptation climatique.
          </li>
        </ul>
      </div>
    </section>
  </div>
</template>
