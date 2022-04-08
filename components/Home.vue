<template>
  <div class="container">
    <h1 class="text-7xl">Vision</h1>

    <div class="selectors">
      <div class="selector" v-for="month in months">
        <button @click="updateMonthsSelected(month)" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
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
        labels: [ 'January', 'February', 'March', 'April', '', '' ],
        datasets: [
          {
            label: "Avis vendus",
            backgroundColor: "hsl(252, 82.9%, 67.8%)",
            borderColor: "hsl(252, 82.9%, 67.8%)",
            data: [40, 20, 12, 50]
          }
        ]
      },
      chartOptions: {
        response: false,
        maintainAspectRatio: false
      },
      months : [
        {
          number: 1,
          label: "Janvier",
          selected: true
        },
        {
          number: 2,
          label: "Février",
          selected: true
        },
        {
          number: 3,
          label: "Mars",
          selected: true
        },
        {
          number: 4,
          label: "Avril",
          selected: true
        }
      ],
      monthsSelected: [
        {
          number: 1,
          label: "Janvier",
          selected: true
        },
        {
          number: 2,
          label: "Février",
          selected: true
        },
        {
          number: 3,
          label: "Mars",
          selected: true
        },
        {
          number: 4,
          label: "Avril",
          selected: true
        }
      ]
    }
  },
  methods: {
    updateMonthsSelected : function (monthToUpdate) {
      console.log(monthToUpdate)

      if (this.monthsSelected.findIndex(month => month.number === monthToUpdate.number)) {
        this.monthsSelected.(this.monthsSelected.findIndex(month => month.number === monthToUpdate.number), 1)
        console.log('if')
      }
      else {
        this.monthsSelected.push(monthToUpdate)
        console.log('else')
      }

    },
    buildData: function () {
      this.chartData.datasets = [
        {
          label: "Avis vendus",
          backgroundColor: "hsl(252, 82.9%, 67.8%)",
          borderColor: "hsl(252, 82.9%, 67.8%)",
          data: [25, 15]
        }
      ]
      console.log(this.chartData.datasets.data)
      this.chartData.labels = ['January', 'February']
      this.chartData.datasets[0].data = [15, 30]
      this.chartData = {...this.chartData}
      console.log(this.chartData.datasets.data)

    },
    buildData2: function () {
      this.chartData.datasets[0].data = [15, 30, 60]
      this.chartData.labels = ['January', 'February', 'March']

      this.chartData = {...this.chartData}
      //this.chartData.datasets = {...this.chartData.datasets}

    }
  },
  computed: {
    updateChart() {

    }
  }
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
    /*max-width: 60em;*/
    margin: auto;
    padding: 1em;
    /*background-color: #212733;*/
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
