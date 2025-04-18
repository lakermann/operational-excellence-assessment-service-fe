<script setup lang="ts">
import { computed } from 'vue'
import {
  Chart as ChartJS,
  RadialLinearScale,
  PointElement,
  LineElement,
  Filler,
  Tooltip,
  Colors,
} from 'chart.js'
import { Radar } from 'vue-chartjs'

ChartJS.register(RadialLinearScale, PointElement, LineElement, Filler, Tooltip, Colors)

export interface Values {
  title: string
  value: number
}

const props = defineProps<{
  values: Values[]
}>()

const data = computed(() => {
  return {
    labels: props.values.map((e) => e.title),
    datasets: [
      {
        label: 'Average',
        data: props.values.map((e) => e.value),
      },
    ],
  }
})

const options = {
  responsive: true,
  maintainAspectRatio: false,
  scales: {
    r: {
      suggestedMin: 0,
      suggestedMax: 5,
      ticks: {
        stepSize: 1,
      },
    },
  },
}
</script>

<template>
  <div class="chart-container">
    <Radar :data="data" :options="options" />
  </div>
</template>

<style scoped>
.chart-container {
  background-color: #ffffff;
  width: 100%;
}

canvas {
  display: block;
}
</style>
