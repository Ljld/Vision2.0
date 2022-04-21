<template>
  <div class="corporate">
    <h1 class="text-6xl">Parts de marché</h1>
    <bar-chart-selector @selectorsUpdated="updateLabels" />
    <div class="my-chart shadow-lg rounded-lg p-10">
      <bar-chart :chart-data="decesChartData" :options="chartOptions" />
    </div>
  </div>
</template>

<script>
import BarChartSelector from "@/components/charts/barChart/barChartSelector";
import BarChart from "@/components/charts/barChart/BarChart";
import {CHART_OPTIONS, MONTHS} from "@/const";

export default {
  name: "corporate",
  components: {BarChart, BarChartSelector},
  data () {
    return {
      chartOptions: CHART_OPTIONS,
      decesChartData: {
        labels: [],
        datasets: [
          {
            label: "Parts de marché",
            backgroundColor: "hsl(252, 82.9%, 67.8%)",
            borderColor: "hsl(252, 82.9%, 67.8%)",
            data: []
          }
        ]
      },
    }
  },
  methods: {
    updateLabels: function (months) {
      months.map(month => {
        if (month.selected) {
          this.decesChartData.labels.push('Décès en ' + month.label)
          this.decesChartData.labels.push('Avis vendus en ' + month.label)
          this.decesChartData.datasets[0].data.push(10)
          this.decesChartData.datasets[0].data.push(5)
        } else {
          this.decesChartData.labels = this.decesChartData.labels.filter(label => {
            return label !== 'Décès en ' + month.label && label !== 'Avis vendus en ' + month.label
          })
        }
      })
      this.decesChartData.datasets[0] = {...this.decesChartData.datasets[0]}
      this.decesChartData = {...this.decesChartData}
      this.decesChartData.labels = {...this.decesChartData.labels}
    }
  }
}
</script>

<style scoped>
.corporate {
  min-height: 80vh;
}
h1 {
  color: #121212;
}
.my-chart {
  max-height: 50em;
  margin: auto;
  padding: 1em;
}
</style>
