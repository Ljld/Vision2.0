<template>
  <div id="content" class="container">
    <div class="selectors">
      <div class="selector" v-for="month in months">
        <button @click="updateChart(month)" :class="getSelectedBtnClass(month)" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
          {{ month.label }}
        </button>
      </div>
    </div>
    <div class="my-chart shadow-lg rounded-lg p-10">
      <BarChart :chart-data="mortsChartData" :options="chartOptions" />
    </div>
    <br><br>
    <div class="my-chart shadow-lg rounded-lg p-10">
      <BarChart :chart-data="avisChartData" :options="chartOptions" />
    </div>
    <br><br>
  </div>
</template>

<script>
import BarChart from "@/components/charts/barChart/BarChart";

export default {
  name: "Home",
  components: { BarChart },
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
          label: "Janvier",
          selected: false,
          avisVendus: 13,
          totalMorts : 0
        },
        {
          number: 2,
          label: "Février",
          selected: false,
          avisVendus: 3,
          totalMorts : 0
        },
        {
          number: 3,
          label: "Mars",
          selected: false,
          avisVendus: 6,
          totalMorts : 0
        },
        {
          number: 4,
          label: "Avril",
          selected: false,
          avisVendus: 4,
          totalMorts : 0
        }
      ]
    }
  },
  methods: {
    updateChart: async function (monthToUpdate) {
      const monthIndex = this.months.findIndex(month => month.number === monthToUpdate.number)

      await this.updateMonths(monthIndex)
      this.updateLabels()
      this.updateChartData()

      this.avisChartData.datasets[0] = {...this.avisChartData.datasets[0]}
      this.avisChartData = {...this.avisChartData}

      this.mortsChartData.datasets[0] = {...this.mortsChartData.datasets[0]}
      this.mortsChartData = {...this.mortsChartData}
    },
    updateMonths: async function (monthIndex) {
      if (monthIndex !== -1) {

        const firstDayOfMonth = new Date(2022, monthIndex, 1).toLocaleDateString()
        const lastDayOfMonth = new Date(2022, monthIndex + 1, 0).toLocaleDateString()

        const params = {
          deathDate: firstDayOfMonth + '-' + lastDayOfMonth,
          aggs: 'deathDate'
        }

        this.months[monthIndex].selected = this.months[monthIndex].selected !== true
        this.months[monthIndex].totalMorts = await this.$axios.$get('agg', {params}).then(response => response.response.total)
      }
    },
    updateLabels: function () {
      this.avisChartData.labels = this.months.filter(month => month.selected).map(month => month.label)
      this.mortsChartData.labels = this.months.filter(month => month.selected).map(month => month.label)
    },
    updateChartData: function () {
      this.avisChartData.datasets[0].data = this.months.filter(month => month.selected).map(month => month.avisVendus)
      this.mortsChartData.datasets[0].data = this.months.filter(month => month.selected).map(month => month.totalMorts)
    },
    getSelectedBtnClass: function (month) {
      return month.selected ? 'selected' : ''
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

  .selected {
    filter: brightness(80%);
  }
</style>
