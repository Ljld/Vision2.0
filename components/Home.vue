<template>
  <div class="container">
    <h1 class="text-7xl">Vision</h1>
    <div class="selectors">
      <div class="selector" v-for="month in months">
        <button @click="updateChart(month)" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
          {{ month.label }}
        </button>
      </div>
    </div>
    <div class="my-chart shadow-lg rounded-lg p-10">
      <BarChart :chart-data="chartData" :options="chartOptions" />
    </div>
    <br><br>
    <div class="my-chart shadow-lg rounded-lg p-10">
      <BarChart :chart-data="chartData" :options="chartOptions" />
    </div>
    <br><br>
  </div>
</template>

<script>
import BarChart from "@/components/BarChart";

export default {
  name: "Home",
  components: { BarChart },
  data () {
    return {
      chartData: {
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
          number: 0,
          label: "Janvier",
          selected: false,
          avisVendus: 13,
          totalMorts : 0
        },
        {
          number: 1,
          label: "Février",
          selected: false,
          avisVendus: 3,
          totalMorts : 0
        },
        {
          number: 2,
          label: "Mars",
          selected: false,
          avisVendus: 6,
          totalMorts : 0
        },
        {
          number: 3,
          label: "Avril",
          selected: false,
          avisVendus: 4,
          totalMorts : 0
        }
      ]
    }
  },
  methods: {
    updateChart: function (monthToUpdate) {
      const monthIndex = this.months.findIndex(month => month.number === monthToUpdate.number)

      this.updateMonths(monthIndex)
      this.updateLabels()
      this.updateChartData()

      this.chartData.datasets[0] = {...this.chartData.datasets[0]}
      this.chartData = {...this.chartData}

      this.getDataTest()

    },
    updateMonths: function (monthIndex) {
      if (monthIndex !== -1) {
        this.months[monthIndex].selected = this.months[monthIndex].selected !== true
      }
    },
    updateLabels: function () {
      this.chartData.labels = this.months.filter(month => month.selected).map(month => month.label)
    },
    updateChartData: function () {
      this.chartData.datasets[0].data = this.months.filter(month => month.selected).map(month => month.avisVendus)
    },
    getDataTest: function () {
       const testData = this.$axios.$get('https://deces.matchid.io/deces/api/v1/agg?birthCity=Paris&aggs=birthCity')
       console.log(testData)
    }
  },
}
</script>

<style scoped>
  h1 {
    margin: 0.5em 0;
    text-align: center;
    color: var(--main-text-color);
  }
  .my-chart {
    max-height: 50em;
    margin: auto;
    padding: 1em;
    background-color: var(--secondary-bg-color-test);
  }
  .selectors {
    display: flex;
    justify-content: center;
  }
  button {
    margin: 1em;
  }
</style>
