<script setup lang="ts">
import * as Plot from '@observablehq/plot'
import * as d3 from 'd3'
import filteredData from '@/assets/filteredData.json' // Assurez-vous que le fichier contient minTemp et maxTemp
import PlotFigure from '@/components/PlotFigure.js'
import climateData3 from '@/assets/climateData3.json'
import { ref } from 'vue'
const timeInterval = ref('Années') // Valeur par défaut

/* const getTimeInterval2 = (aaaamm, interval) => {
  let year = +String(aaaamm).slice(0, 4);
  if (interval === "Décennies") return Math.floor(year / 10) * 10;
  if (interval === "5 ans") return Math.floor(year / 5) * 5;
  return year;
} */
</script>

<template>
  <section class="p-7 lg:px-36">
    <h1 class="mb-6">le Lot-et-Garonne : un aperçu des changements climatiques de 1950 à 2022</h1>
    <p class="mb-4">
      Nous avons choisi de concentrer notre étude sur le Lot-et-Garonne, une région qui se distingue
      par une température moyenne de 20,27°C sur la période analysée. Ce département, situé dans le
      sud-ouest de la France, présente des conditions climatiques marquées par des étés chauds et
      des hivers doux. Sa position géographique fait de cette région un excellent exemple des
      tendances générales observées dans le cadre du réchauffement climatique en France.
    </p>
    <p class="mb-9">
      De plus, en raison de sa situation entre les zones côtières et les terres plus continentales,
      le Lot-et-Garonne subit à la fois les effets des changements climatiques affectant l'ensemble
      du pays et des spécificités locales, ce qui en fait un indicateur pertinent pour évaluer
      l'impact du réchauffement à une échelle régionale.
    </p>
    <div class="flex justify-center mb-9">
      <PlotFigure
        :options="{
          title: 'Évolution des températures dans le Lot-et-Garonne',
          subtitle: 'Températures minimales et maximales de 1950 à 2022',
          width: 1100,
          height: 400,
          marginLeft: 100,
          marginBottom: 50,
          marks: [
            Plot.areaY(filteredData, {
              x: 'Année',
              y1: 'minTemp', // Température minimale
              y2: 'maxTemp', // Température maximale
              fill: '#FF8C00',
              fillOpacity: 0.5
            }),
            Plot.line(filteredData, {
              x: 'Année',
              y: 'minTemp',
              stroke: 'blue',
              strokeWidth: 1
            }),
            Plot.line(filteredData, {
              x: 'Année',
              y: 'maxTemp',
              stroke: '#FF8C00',
              strokeWidth: 1
            }),
            Plot.dot(filteredData, {
              x: 'Année',
              y: 'minTemp',
              fill: 'blue',
              tip: true
            }),
            Plot.dot(filteredData, {
              x: 'Année',
              y: 'maxTemp',
              fill: '#FF8C00',
              tip: true
            })
          ],
          x: { label: 'Année' },
          y: { label: 'Température (°C)' }
        }"
      />
    </div>

    <h3 class="mb-3">Analyse des tendances</h3>
    <h4 class="mb-2">1. Températures maximales</h4>
    <ul class="list-disc list-inside">
      <li class="mb-2">
        Augmentation progressive : On observe une tendance à la hausse des températures maximales.
        Par exemple, des années comme 1991, 2003, et 2022 ont vu des pics élevés (36°C, 38°C, et
        36.9°C respectivement), indiquant potentiellement des vagues de chaleur plus fréquentes ou
        plus intenses ces dernières décennies.
      </li>
      <li class="mb-2">
        Années marquantes : 2003 est l’année la plus chaude avec une température maximale de 38°C,
        marquant l'une des périodes les plus chaudes en France, liée à une canicule historique.
      </li>
      <li class="mb-3">
        Réchauffement global : Cette augmentation des températures maximales pourrait être
        interprétée comme un effet du réchauffement climatique, où les étés tendent à devenir plus
        chauds avec des périodes de chaleur plus extrêmes.
      </li>
    </ul>
    <h4 class="mb-2">2. Températures minimales</h4>
    <ul class="list-disc list-inside">
      <li class="mb-2">
        Variabilité notable : Les températures minimales varient de façon assez marquée, avec des
        hivers très froids notamment en 1956 (-13.2°C) et 1987 (-9°C). Cependant, ces grands
        froids sont moins fréquents après les années 1980.
      </li>
      <li class="mb-4">
        Adoucissement des hivers : Depuis les années 1990, les hivers semblent légèrement plus
        doux en moyenne, bien que certaines années comme 2012 (-8.6°C) montrent encore des
        épisodes de froid important.
      </li>
    </ul>
    <h3 class="mb-3">Évolutions et régularités</h3>
    <ul class="list-disc list-inside">
      <li class="mb-2">
        Décalage des extrêmes : Il est intéressant de noter que si les hivers froids persistent,
        la tendance à l'augmentation des températures maximales est plus prononcée, ce qui
        pourrait signaler une plus grande fréquence des étés chauds, tandis que les hivers restent
        globalement froids, mais avec des épisodes extrêmes plus rares.
      </li>
      <li class="mb-2">
        Variabilité interannuelle : Le graphique montre une variabilité assez importante d'une année
        à l'autre, avec des années plus modérées suivies d'années plus extrêmes. Par exemple,
        entre 2011 et 2014, les variations sont modérées, tandis que 2015-2017 montre des pics de
        chaleur plus prononcés.
      </li>
    </ul>
  </section>
</template>