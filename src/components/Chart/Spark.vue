<template>
   <div class="spark-demo">
     <h2> Spark </h2>
     <apexcharts height="160" type="area" :options="options" :series="series"></apexcharts>
   </div>
</template>


<script>
import VueApexCharts from "vue-apexcharts";

const randomizeArray = function(arg) {
  var array = arg.slice();
  var currentIndex = array.length,
    temporaryValue,
    randomIndex;
  while (0 !== currentIndex) {
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex -= 1;
    temporaryValue = array[currentIndex];
    array[currentIndex] = array[randomIndex];
    array[randomIndex] = temporaryValue;
  }
  return array;
};

// data for the sparklines that appear below header area
var sparklineData = [
  47,
  45,
  54,
  38,
  56,
  24,
  65,
  31,
  37,
  39,
  62,
  51,
  35,
  41,
  35,
  27,
  93,
  53,
  61,
  27,
  54,
  43,
  19,
  46
];

export default {
  components: {
    apexcharts: VueApexCharts
  },
  data() {
    return {
      options: {
        chart: {
          type: "area",
          height: 160,
          sparkline: {
            enabled: true
          }
        },
        stroke: {
          curve: "straight"
        },
        fill: {
          opacity: 0.3,
          gradient: {
            enabled: false
          }
        },
        series: [
          {
            data: randomizeArray(sparklineData)
          }
        ],
        yaxis: {
          min: 0
        },
        colors: ["#DCE6EC"],
        title: {
          text: "$424,652",
          offsetX: 0,
          style: {
            fontSize: "24px",
            cssClass: "apexcharts-yaxis-title"
          }
        },
        subtitle: {
          text: "Sales",
          offsetX: 0,
          style: {
            fontSize: "14px",
            cssClass: "apexcharts-yaxis-title"
          }
        }
      },
      series: [
        {
          data: randomizeArray(sparklineData)
        }
      ]
    };
  }
};
</script>
