<script setup lang="ts">
import * as Plot from "@observablehq/plot";
import filteredTemp from "@/assets/filteredTemp.json";
import filteredConso from "@/assets/filteredConso.json";
import PlotFigure from "@/components/PlotFigure.js";
</script>

<template>
  <section class="p-7 lg:px-36">
    <h1 class="mb-6">Évolution des températures et de la consommation d'énergie</h1>
    <div class="flex justify-center mb-6">
      <PlotFigure
        :options="{
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
                r: 15,
                fillOpacity: 0.7,
                stroke: 'orange' // Changer la couleur de la bordure des points
              }
            )
          ],
          x: { label: 'Année' },
          y: { label: 'Température Moyenne (°C)' },
          color: {
            legend: true,
            label: 'Consommation d\'énergie (kWh)',
            scheme: 'oranges'
          }
        }"
      />
    </div>
    <div class="p-7 lg:px-36">
      <h3 class="mb-3">Analyse</h3>
      <h4 class="mb-2">1. Tendance générale</h4>
      <p class="">
        Températures élevées et consommation d'énergie accrue : Les années où les températures maximales sont les plus élevées (comme 2012 et 2022) correspondent à des points plus grands et plus foncés, indiquant une consommation d'énergie plus élevée. Cela suggère une corrélation positive : à mesure que la température maximale augmente, la consommation d'énergie tend à augmenter. Cela est probablement dû à une plus forte utilisation de systèmes de climatisation ou d'autres moyens de rafraîchissement qui nécessitent davantage d'énergie.
      </p>
      <h4 class="mb-2">2. Années avec des températures plus basses</h4>
      <p class="">
        En revanche, pour des années comme 2014 et 2020, où les températures maximales sont plus basses (en dessous de 32°C), les points sont plus petits et plus clairs, ce qui montre une consommation d'énergie plus faible. Cela renforce l'idée que des températures plus modérées entraînent une demande énergétique moins importante.
      </p>
      <h4 class="mb-2">3. Températures modérées et consommation plus variable</h4>
      <p class="">
        Les années avec des températures moyennes modérées (entre 31°C et 33°C), comme 2013, 2017, et 2019, montrent des points de taille intermédiaire. Ces années illustrent que la consommation d'énergie ne suit pas strictement une courbe linéaire en fonction des températures. D'autres facteurs, comme les politiques énergétiques, les habitudes de consommation, ou les conditions météorologiques spécifiques (canicules, périodes de froid, etc.), peuvent également jouer un rôle.
      </p>
      <h4 class="mb-2">4. Linéarité de la corrélation</h4>
      <p class="">
        Bien qu'il y ait une corrélation positive globale entre les températures maximales et la consommation d'énergie, celle-ci n'est pas parfaitement linéaire. Par exemple, la consommation d'énergie en 2020 est relativement faible malgré des températures proches de celles de 2019. Cela montre que la température maximale n'est pas l’unique facteur déterminant la consommation d'énergie, bien qu'elle joue un rôle important.
      </p>
      <h3 class="mb-3">Interprétation globale</h3>
      <p>
        Il est clair que lorsque les températures augmentent, surtout au-delà de 33-34°C, la consommation d'énergie connaît une hausse notable. Cela pourrait s'expliquer par une augmentation des besoins énergétiques pour maintenir le confort dans les bâtiments via la climatisation, notamment pendant les étés de plus en plus chauds. Toutefois, la corrélation n'est pas parfaitement linéaire, ce qui laisse supposer que d'autres facteurs, comme la technologie, les habitudes de consommation ou les infrastructures énergétiques, influencent également la consommation.
      </p>
      <h3 class="mb-3">Conclusion</h3>
      <p>
        La corrélation observée dans ce graphique montre bien que les hautes températures favorisent une augmentation de la consommation d'énergie, mais cette relation est modérée par d'autres influences. Cela souligne l'importance de comprendre le rôle de la température dans les besoins énergétiques futurs et de s'adapter à cette réalité dans un contexte de changement climatique.
      </p>
    </div>
  </section>
</template>