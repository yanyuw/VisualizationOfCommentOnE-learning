<template>
  <div class="wordcloud">
    <div id="wordcloud" class="container"></div>
  </div>
</template>

<script>
import "echarts-wordcloud/dist/echarts-wordcloud";
export default {
  name: "Wordcloud",
  mounted() {
    this.initChart();
  },
  methods: {
    initChart() {
      let emotionsJson = require("../assets/weibo-word-emotion.json");
      let data = emotionsJson.map(val => {
        return {
          name: val["word"],
          value: val["freq"]
        };
      });

      let myChart = this.$echarts.init(document.getElementById("wordcloud"));
      const option = {
        title: {
          text: "舆论词云",
          x: "center",
          textStyle: {
            color: "#fff",
            fontSize: 22
          }
        },
        toolbox: {
          feature: {
            // mark: { show: true },
            // dataView: {
            //   show: true,
            //   readOnly: false
            // },
            // restore: { show: true },
            saveAsImage: { show: true },
          }
        },
        // backgroundColor: "rgba(230, 220, 220, 0.4)",
        // tooltip: {
        //   pointFormat: "{series.name}: <b>{point.percentage:.1f}%</b>"
        // },
        series: [
          {
            type: "wordCloud",
            //用来调整词之间的距离
            gridSize: 10,
            //用来调整字的大小范围
            sizeRange: [14, 60],
            //用来调整词的旋转方向，，[0,0]--代表着没有角度，也就是词为水平方向，需要设置角度参考注释内容
            // rotationRange: [-45, 0, 45, 90],
            // rotationRange: [ 0,90],
            rotationRange: [0, 30],
            //随机生成字体颜色
            // maskImage: maskImage,
            textStyle: {
              normal: {
                color: function() {
                  return (
                    "rgb(" +
                    Math.round(Math.random() * 255) +
                    ", " +
                    Math.round(Math.random() * 255) +
                    ", " +
                    Math.round(Math.random() * 255) +
                    ")"
                  );
                }
              }
            },
            //位置相关设置
            left: "center",
            top: 20,
            right: null,
            bottom: null,
            width: "100%",
            height: "100%",
            //数据
            data: data
          }
        ]
      };
      myChart.setOption(option);
    }
  }
};
</script>
<style  scoped>
.chartsClass {
  padding-left: 1.2rem;
}
.wordcloud {
  /* position: absolute;
  bottom: 0;
  left: 50px; */
}
</style>