<template>
   <div>
     <h2> VueApexCharts </h2>
     <apexcharts width="500" type="bar" :options="options" :series="series"></apexcharts>
   </div>
</template>

<script>
import VueApexCharts from "vue-apexcharts";
export default {
  components: {
    apexcharts: VueApexCharts
  },
  props: {
    options: {
      type: Object
    },
    series: {
      type: Array
    }
  }
};
</script>
