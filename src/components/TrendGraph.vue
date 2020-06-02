<template>
  <div class="trend">
    <div id="graph1" class="container"></div>
  </div>
</template>

<script>
export default {
  name: "TrendGraph",
  mounted() {
    this.draw()
  },
  methods: {
    draw() {
      let trendJson = require("../assets/trend.json");

      
      let myChart = this.$echarts.init(document.getElementById('graph1'))
      // var app = {};
      myChart.setOption( {
        title: {
          text: "微博指数"
        },
        tooltip: {
          trigger: "axis"
        },
        legend: {
          data: ["微博"]
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: trendJson["data"]["x"]
        },
        yAxis: {
          type: "value"
        },
        series: [
          {
            name: "微博",
            type: "line",
            stack: "总量",
            data: trendJson["data"]["s"]
          },
        ]
      })
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
