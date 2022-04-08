<template>
</template>

<script>

export default {
  name: "AvisChart",
  data () {
    return {
      chartData: {
        labels: [ 'January', 'February', 'March' ],
        datasets: [ { data: [40, 20, 12] } ]
      },
      chartOptions: {
        responsive: true
      }
    }
  }
}
</script>

<style scoped>

</style>
