<!-- eslint-disable vue/multi-word-component-names -->

<script setup>
import { ref, computed } from 'vue'
import * as Plot from '@observablehq/plot'
import PlotFigure from '@/components/PlotFigure.js'
import climateData3 from '@/assets/climateData3.json'

const timeInterval = ref('Décennies')

const filteredData = computed(() => {
  console.log('filteredData timeInterval :', timeInterval.value)
  const data = climateData3.filter((d) => {
    const year = d.interval
    if (timeInterval.value === 'Décennies') {
      return year % 10 === 0
    } else if (timeInterval.value === '5 ans') {
      return year % 5 === 0
    }
    return true
  })
  console.log('filteredData return :', data)

  return data
})

const chartOptions = computed(() => ({
  width: 1000,
  height: 600,
  marginLeft: 100,
  marginRight: 100,
  marginBottom: 70,
  title: `Durée d'ensoleillement dans le Lot-et-Garonne (${timeInterval.value})`,
  x: {
    label: timeInterval.value,
    tickFormat: (d) => (timeInterval.value === 'Décennies' ? `${d}s` : d),
    domain: filteredData.value.map((d) => d.interval),
    ticks: filteredData.value.map((d) => d.interval)
  },
  y: {
    label: "Durée d'ensoleillement (heures)",
    grid: true
  },
  marks: [
    Plot.barY(filteredData.value, {
      x: 'interval',
      y: 'INST',
      fill: '#FF8000',
      tip: {
        format: {
          x: (d) => (timeInterval.value === 'Décennies' ? `${d}s` : d),
          y: (d) => `Ensoleillement: ${d.INST.toFixed(0)} heures`
        }
      },
      title: (d) => `Ensoleillement: ${d.INST.toFixed(0)} heures,
        Temp. max: ${d.avgTX.toFixed(1)}°C
        Temp. min: ${d.avgTN.toFixed(1)}°C`
    }),
    Plot.ruleY([0])
  ],
  color: {
    domain: ['Ensoleillement'],
    range: ['#FF8000'],
    legend: true
  }
}))
</script>

<template>
  <PlotFigure :key="timeInterval" :options="chartOptions" />
</template>
