<template>
  <div class="corporate">
    <h1 class="text-6xl">Parts de marché</h1>
    <bar-chart-selector />
    <bar-chart />
  </div>
</template>

<script>
import BarChartSelector from "@/components/charts/barChart/barChartSelector";
import BarChart from "@/components/charts/barChart/BarChart";
export default {
  name: "corporate",
  components: {BarChart, BarChartSelector}
}
</script>

<style scoped>

</style>
