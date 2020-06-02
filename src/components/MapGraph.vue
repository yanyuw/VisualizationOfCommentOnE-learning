<template>
  <div class="map">
    <div id="map" class="whole-conatiner"></div>
  </div>
</template>

<script>

import '../../node_modules/echarts/map/js/china.js' // 引入中国地图数据
export default {
  name: "MapGraph",
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      let data = require("../assets/weibo-map.json");

      console.log(data)
      let myChart = this.$echarts.init(document.getElementById("map"));
      myChart.setOption({
        title: {
          text: "舆论地点分布",
          subtext: "",
          left: "center"
        },
        tooltip: {
          trigger: "item"
        },
        legend: {
          orient: "vertical",
          left: "left",

          top: "middle",
          data: ["舆论指数", ]
        },
        visualMap: {
          min: 0,
          max: 1,
          left: "left",
          top: "bottom",
          text: ["积极", "消极"], // 文本，默认为数值文本
          calculable: true
        },
        toolbox: {
          show: true,
          orient: "vertical",
          left: "right",
          top: "center",
          feature: {
            mark: { show: true },
            dataView: { show: true, readOnly: false },
            restore: { show: true },
            saveAsImage: { show: true }
          }
        },
        series: [
          {
            name: "舆论指数",
            type: "map",
            mapType: "china",
            roam: false,
            label: {
              normal: {
                show: false
              },
              emphasis: {
                show: true
              }
            },
            data: data
          },
        ]
      });
    }
  }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.whole-conatiner{
  width: 95vw;
  height: 100vh;
}
.map{
  position: absolute;
    top: 0;
}
</style>
