<script setup lang="ts">
import * as Plot from '@observablehq/plot'
import filteredData from '@/assets/filteredData.json' // Assurez-vous que le fichier contient minTemp et maxTemp
import PlotFigure from '@/components/PlotFigure.js'
</script>

<template>
  <h1>Évolution des températures minimales et maximales</h1>
  <PlotFigure
    :options="{
      title: 'Évolution des températures dans le Lot-et-Garonne',
      subtitle: 'Températures minimales et maximales de 1950 à 2022',
      width: 800,
      height: 400,
      marginLeft: 100,
      marginBottom: 50,
      marks: [
        Plot.areaY(filteredData, {
          x: 'Année',
          y1: 'minTemp', // Température minimale
          y2: 'maxTemp', // Température maximale
          fill: 'lightcoral',
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
          stroke: 'red',
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
</template>
