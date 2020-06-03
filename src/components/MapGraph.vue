<template>
  <div class="map">
    <div id="map" class="whole-conatiner"></div>
  </div>
</template>

<script>
import "../../node_modules/echarts/map/js/china.js"; // 引入中国地图数据
export default {
  name: "MapGraph",
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      let data = require("../assets/weibo-map.json");

      // console.log(data);
      let myChart = this.$echarts.init(document.getElementById("map"));
      myChart.setOption({
        title: {
          text: "舆论地点分布",
          subtext: "",
          x: "center",
          y: "bottom",
          textStyle: {
            color: "#fff",
            fontSize: 22
          }
        },
        tooltip: {
          trigger: "item"
        },
        legend: {
          orient: "vertical",
          left: "left",

          top: "middle",
          data: ["舆论指数"],
          textStyle: {
            color: "#00eeff"
          }
        },
        visualMap: {
          // color: "#00eeff",
          min: 0,
          max: 1,
          left: 400,
          top: "bottom",
          text: ["积极", "消极"], // 文本，默认为数值文本
          calculable: true,
          textStyle: {
            color: "#00eeff"
          },
          inRange: {
            // 选中范围中的视觉配置
            color: ["#63ADD0", "#086FA1", "#034769"], // 定义了图形颜色映射的颜色列表，
            // 数据最小值映射到'blue'上，
            // 最大值映射到'red'上，
            // 其余自动线性计算。
            symbolSize: [0, 1] // 定义了图形尺寸的映射范围，
            // 数据最小值映射到30上，
            // 最大值映射到100上，
            // 其余自动线性计算。
          }
        },
        toolbox: {
          show: true,
          orient: "vertical",
          // left: 200,
          right: 400,
          top: "center",
          feature: {
            mark: { show: true },
            // dataView: { show: true, readOnly: false },
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
            itemStyle: {
              normal: {
                //未选中状态
                // borderWidth: 2, //边框大小
                // borderColor: "lightgreen",
                areaColor: "rgb(255,255,255,0.5)", //背景颜色
                label: {
                  show: true //显示名称
                }
              },
              emphasis: {
                // 也是选中样式
                borderWidth: 2,
                borderColor: "#fff",
                areaColor: "#00B060",
                label: {
                  show: true,
                  textStyle: {
                    color: "#fff"
                  }
                }
              }
            },
            label: {
              normal: {
                show: false
              },
              emphasis: {
                show: true
              }
            },
            data: data
          }
        ]
      });
    }
  }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.whole-conatiner {
  width: 80%;
  height: 80%;
  margin-left: 10%;
  margin-top: 8%;
}
.map {
  position: absolute;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: -999;
}
</style>
