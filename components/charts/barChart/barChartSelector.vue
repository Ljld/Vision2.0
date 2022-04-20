<template>
  <div class="selectors">
    <div class="selector month-selector" v-for="month in months">
      <button @click="month.selected = !month.selected" :class="() => month.selected ? 'active' : ''" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
        {{ month.label }}
      </button>
    </div>
  </div>
</template>

<script>
import { MONTHS } from '@/const'

export default {
  name: "barChartSelector",
  data () {
    return {
      avisChartData: {
        labels: [],
        datasets: [
          {
            label: "Avis vendus",
            backgroundColor: "hsl(252, 82.9%, 67.8%)",
            borderColor: "hsl(252, 82.9%, 67.8%)",
            data: []
          }
        ]
      },
      mortsChartData: {
        labels: [],
        datasets: [
          {
            label: "Morts en France",
            backgroundColor: "hsl(252, 82.9%, 67.8%)",
            borderColor: "hsl(252, 82.9%, 67.8%)",
            data: []
          }
        ]
      },
      chartOptions: {
        response: false,
        maintainAspectRatio: false,
        scales: {
          yAxes: [{
            ticks: {
              min: 0,
            }
          }]
        }
      },
      months : [
        {
          number: 1,
          label: MONTHS.JANUARY,
          selected: false,
          value: 0
        },
        {
          number: 2,
          label: MONTHS.FEBRUARY,
          selected: false,
          value: 0
        },
        {
          number: 3,
          label: MONTHS.MARCH,
          selected: false,
          value: 0
        },
        {
          number: 4,
          label: MONTHS.APRIL,
          selected: false,
          value: 0
        }
      ]
    }
  },
}
</script>

<style scoped>

</style>
