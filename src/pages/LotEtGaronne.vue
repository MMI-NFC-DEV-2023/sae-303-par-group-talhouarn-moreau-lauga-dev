<script setup lang="ts">
import * as Plot from '@observablehq/plot'
import * as d3 from 'd3'
import filteredData from '@/assets/filteredData.json' // Assurez-vous que le fichier contient minTemp et maxTemp
import PlotFigure from '@/components/PlotFigure.js'
import climateData3 from '@/assets/climateData3.json'
import { ref } from 'vue'
import filteredTemp from '@/assets/filteredTemp.json'
import filteredConso from '@/assets/filteredConso.json'
import Ensoleillement from '@/components/ensoleillement.vue'
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
      Nous avons choisi de concentrer notre étude sur le Lot-et-Garonne, un departement qui se distingue
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
              fill: 'orange',
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
              stroke: 'orange',
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
              fill: 'red',
              tip: true
            })
          ],
          x: { label: 'Année' },
          y: { label: 'Température (°C)' }
        }"
      />
    </div>
    <a  href="https://explore.data.gouv.fr/fr/datasets/6569af36ba0c3d2f9d4bf98c/#/resources/33dc01bc-1c8b-4e5d-bfcd-185ffe2db682">Données graphique</a>
    <h3 class="mb-3 mt-4">Analyse des tendances</h3>
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

  
  <section class="p-7 lg:px-36">
    <h1 class="mb-5 lg:mb-7">La hausse des températures et ses conséquences énergétiques dans le Lot et Garonne</h1>
    <p class="mb-4">
      Au fil des années, les changements climatiques se traduisent par une augmentation des
      températures moyennes, avec des impacts significatifs sur divers secteurs. Parmi ceux-ci, la
      consommation d'énergie est particulièrement sensible aux fluctuations climatiques. En effet,
      des températures plus élevées entraînent une demande croissante en énergie, notamment pour le
      refroidissement des bâtiments et la climatisation.
    </p>
    <p class="mb-4">
      Cette tendance soulève des questions importantes sur la manière dont nous gérons nos
      ressources énergétiques face aux défis climatiques. Une analyse approfondie des températures
      maximales et de la consommation d'énergie peut nous aider à mieux comprendre cette dynamique
      et à anticiper les besoins futurs.
    </p>
    <p class="mb-10">
      Voyons maintenant comment ces facteurs interagissent à travers une représentation visuelle des
      données.
    </p>
    <h2 class="mb-4">Corrélation entre les températures maximales et la consommation d'énergie de 2012 à 2022</h2>
    <h3 class="mb-7">La consommation d'énergie en KWh pour chaque année, par rapport aux températures maximales dans le Lot-et-Garonne</h3>
    <div class="mb-6 flex justify-center">
      <PlotFigure
        :options="{
          width: 800,
          height: 400,
          marks: [
            Plot.dot(
              filteredTemp.map((temp, index) => ({
                year: temp.Année,
                temperature: temp.maxTemp,
                energyConsumption: filteredConso[index].TotaleConso
              })),
              {
                x: 'year',
                y: 'temperature',
                fill: 'energyConsumption',
                tip: true,
                r: 5,
                fillOpacity: 0.7,
              }
            )
          ],
          x: { label: 'Année', grid: true },
          y: { label: 'Température Moyenne (°C)', grid: true },
          color: {
            legend: true,
            label: 'Consommation d\'énergie (kWh)',
            scheme: 'oranges',
            grid: {
              display: true
            }
          
          }
        }"
      />
      
    </div>
    <div>
      <p class="mt-3 mb-2">Sources</p>
      <a href="https://odre.opendatasoft.com/explore/dataset/conso-departement-annuelle/table/?disjunctive.libelle_departement&disjunctive.libelle_region&disjunctive.e_operateurs&disjunctive.g_operateurs&sort=-libelle_departement">Source 1</a>
      <a href="https://explore.data.gouv.fr/fr/datasets/6569af36ba0c3d2f9d4bf98c/#/resources/33dc01bc-1c8b-4e5d-bfcd-185ffe2db682"> Source 2</a>
      <h3 class="mb-5 mt-10">Analyse</h3>
      <h4 class="mb-4">1. Tendance générale</h4>
      <p class="mb-4">
        Températures élevées et consommation d'énergie accrue : Les années où les températures
        maximales sont les plus élevées (comme 2012 et 2022) correspondent à des points plus foncés, indiquant une consommation d'énergie plus élevée. Cela suggère une
        corrélation positive : à mesure que la température maximale augmente, la consommation
        d'énergie tend à augmenter. Cela est probablement dû à une plus forte utilisation de
        systèmes de climatisation ou d'autres moyens de rafraîchissement qui nécessitent davantage
        d'énergie.
      </p>
      <h4 class="mb-4">2. Années avec des températures plus basses</h4>
      <p class="mb-4">
        En revanche, pour des années comme 2014 et 2020, où les températures maximales sont plus
        basses (en dessous de 32°C), les points sont plus clairs, ce qui montre une
        consommation d'énergie plus faible. Cela renforce l'idée que des températures plus modérées
        entraînent une demande énergétique moins importante.
      </p>
      <h4 class="mb-4">3. Températures modérées et consommation plus variable</h4>
      <p class="mb-4">
        Les années avec des températures moyennes modérées (entre 31°C et 33°C), comme 2013, 2017,
        et 2019, montrent des points de couleurs intermédiaire. Ces années illustrent que la
        consommation d'énergie ne suit pas strictement une courbe linéaire en fonction des
        températures. D'autres facteurs, comme les politiques énergétiques, les habitudes de
        consommation, ou les conditions météorologiques spécifiques (canicules, périodes de froid,
        etc.), peuvent également jouer un rôle.
      </p>
      <h3 class="mb-4">Interprétation globale</h3>
      <p class="mb-4">
        Il est clair que lorsque les températures augmentent, surtout au-delà de 33-34°C, la
        consommation d'énergie connaît une hausse notable. Cela pourrait s'expliquer par une
        augmentation des besoins énergétiques pour maintenir le confort dans les bâtiments via la
        climatisation, notamment pendant les étés de plus en plus chauds. Toutefois, la corrélation
        n'est pas parfaitement linéaire, ce qui laisse supposer que d'autres facteurs, comme la
        technologie, les habitudes de consommation ou les infrastructures énergétiques, influencent
        également la consommation.
      </p>
      <h3 class="mb-3">Conclusion</h3>
      <p>
        La corrélation observée dans ce graphique montre bien que les hautes températures favorisent
        une augmentation de la consommation d'énergie, mais cette relation est modérée par d'autres
        influences. Cela souligne l'importance de comprendre le rôle de la température dans les
        besoins énergétiques futurs et de s'adapter à cette réalité dans un contexte de changement
        climatique.
      </p>
      
    </div>
    <div>
      <h1 class="mb-5 mt-10 lg:mb-7">Les journées d'ensoleillement</h1>
      <Ensoleillement />
    </div>
  </section>

</template>