<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, computed } from 'vue'
import * as Plot from '@observablehq/plot'
import PlotFigure from '@/components/PlotFigure.js'
import precipitationData from '@/assets/precipitationGrouped.json'

const selectedYear = ref(2022)

const selectedYearData = computed(() => {
  return precipitationData.find((item) => item.year === selectedYear.value) || { communes: [] }
})

const chartOptions = computed(() => ({
  width: 800,
  height: 500,
  marginLeft: 200,
  marginBottom: 50,
  x: {
    label: 'Précipitations (mm)',
    grid: true
  },
  y: {
    label: 'Communes',
    padding: 0.5
  },
  marks: [
    Plot.barX(
      selectedYearData.value.communes.map((commune) => ({
        name: commune[0],
        precipitation: commune[1]
      })),
      {
        x: 'precipitation',
        y: 'name',
        fill: '#ff8000',
        title: (d) => `Précipitation: ${d.precipitation} mm`
      }
    )
  ]
}))

const sortedYears = computed(() => {
  return precipitationData.map((d) => d.year).sort((a, b) => a - b)
})
</script>

<template>
  <h2 class="mt-4 font-semibold">Les précipitations pour l'année {{ selectedYear }}</h2>
  <h3 class="font-normal">
    Moyennes de la hauteur des précipitations en mm pour chaque commune dans le Lot-et-Garonne
  </h3>
  <PlotFigure :options="chartOptions" :key="selectedYear" />
  <select v-model="selectedYear" class="rounded-sm border border-black bg-orange-50 px-2">
    <option v-for="year in sortedYears" :key="year" :value="year">
      {{ year }}
    </option>
  </select>
</template>
