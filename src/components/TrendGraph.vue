<template>
  <div class="trend">
    <div id="graph1" class="container"></div>
  </div>
</template>

<script>
export default {
  name: "TrendGraph",
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      let trendJson = require("../assets/trend.json");

      let myChart = this.$echarts.init(document.getElementById("graph1"));
      // var app = {};
      const option = {
        title: {
          text: "微博指数",
          textStyle: {
            fontSize: 20, //字体大小
            color: "#ffffff" //字体颜色
          },
          x: "center"
        },
        tooltip: {
          trigger: "axis"
        },
        legend: {
          data: ["微博"],
          x: "left",
          y: 20,
          textStyle: {
            color: "#00eeff" // 图例文字的颜色
          }
        },
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        toolbox: {
          feature: {
            mark: { show: true },
            dataView: {
              show: true,
              readOnly: false,
            },
            // restore: { show: true },
            saveAsImage: { show: true },
            magicType: { type: ["line", "bar"] }
          }
        },
        xAxis: {
          type: "category",
          boundaryGap: false,
          data: trendJson["data"]["x"],
          axisLabel: {
            textStyle: {
              color: "#7edae8" //坐标的字体颜色
            }
          }
        },
        yAxis: {
          type: "value",
          axisLabel: {
            textStyle: {
              color: "#7edae8" //坐标的字体颜色
            }
          }
        },
        series: [
          {
            name: "微博",
            type: "line",
            stack: "总量",
            data: trendJson["data"]["s"]
          }
        ]
      };

      myChart.setOption(option);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.trend {
}
</style>
