<template>
  <div class="trend">
    <div id="weibo-trend" class="container"></div>
  </div>
</template>

<script>
export default {
  name: "EmotionTrendGraph",
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      let trendJson = require("../assets/weibo-trend.json");
      let timeArr = trendJson.map(val => {
        return val["time"];
      });
      let senArr = trendJson.map(val => {
        return val["sentiments"];
      });

      let myChart = this.$echarts.init(document.getElementById("weibo-trend"));
      // var app = {};
      myChart.setOption({
        title: {
          text: "微博舆论情感态度倾向变化",
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
          data: timeArr,
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
            data: senArr
          }
        ]
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.trend {
  /* position: absolute;
  right: 0; */
}
</style>
