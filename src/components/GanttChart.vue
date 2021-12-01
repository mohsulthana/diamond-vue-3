<template>
<div id="chart">
  <div class="p-grid">
    <div class="p-col-12">
      <div class="card no-gutter">
        <apexcharts type="rangeBar" height="350" :options="chartOptions" :series="series"></apexcharts>
      </div>
    </div>
  </div>
</div>
</template>

<script>
import Apexcharts from "vue3-apexcharts";

export default {
  data: function () {
    return {
      series: [{
        data: [{
            x: 'Code',
            y: [
              new Date('2019-03-02').getTime(),
              new Date('2019-03-04').getTime()
            ]
          },
          {
            x: 'Test',
            y: [
              new Date('2019-03-04').getTime(),
              new Date('2019-03-08').getTime()
            ]
          },
          {
            x: 'Validation',
            y: [
              new Date('2019-03-08').getTime(),
              new Date('2019-03-12').getTime()
            ]
          },
          {
            x: 'Deployment',
            y: [
              new Date('2019-03-12').getTime(),
              new Date('2019-03-18').getTime()
            ]
          }
        ]
      }],
      chartOptions: {
        chart: {
          height: 350,
          type: 'rangeBar'
        },
        plotOptions: {
          bar: {
            horizontal: true
          }
        },
        xaxis: {
          type: 'datetime'
        }
      },
    };
  },
  name: "Gantt Chart",
  components: {
    Apexcharts
  },
};
</script>
