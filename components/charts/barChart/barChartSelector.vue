<template>
  <div class="selectors">
    <div class="year-selectors">
      <div class="selector year-selector">
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full active">
          2022
        </button>
      </div>
    </div>
    <div class="month-selectors">
      <div class="selector month-selector" v-for="month in months">
        <button @click="handleSelectorClick(month)" :class="month.selected ? 'active' : ''" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-full">
          {{ month.label }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { MONTHS } from '@/const'

export default {
  name: "barChartSelector",
  data () {
    return {
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
  methods: {
    handleSelectorClick: function (month) {
      month.selected = month.selected!==true
      this.$emit('selectorsUpdated', this.months)
    }
  }
}
</script>

<style scoped>
.year-selectors, .month-selectors {
  display: flex;
  justify-content: center;
}
.active {
  filter: brightness(80%);
}
button {
  margin: 1em;
}
</style>
