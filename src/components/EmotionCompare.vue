<template>
  <div class="compare">
    <div id="compare" class="container"></div>
  </div>
</template>

<script>
export default {
  name: "EmotionCompare",
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      let emotionsJson = require("../assets/weibo-emotions.json");
      let _00emotion = [0, 0, 0];
      let _90emotion = [0, 0, 0];
      let _80emotion = [0, 0, 0];
      let _70emotion = [0, 0, 0];
      emotionsJson.map(val => {
        if (val["age"] == 0 || (val["age"] <= 30 && val["age"] > 20)) {
          _90emotion[this.getEmotion(val["sentiments"])]++;
        } else if (val["age"] <= 40 && val["age"] > 30) {
          _80emotion[this.getEmotion(val["sentiments"])]++;
        } else if (val["age"] <= 50 && val["age"] > 40) {
          _70emotion[this.getEmotion(val["sentiments"])]++;
        } else if (val["age"] <= 20 && val["age"] > 10) {
          _00emotion[this.getEmotion(val["sentiments"])]++;
        }
      });
      console.log(_00emotion);

      let myChart = this.$echarts.init(document.getElementById("compare"));

      myChart.setOption({
        title: {
          text: "情感态度年龄对比"
        },
        tooltip: {},
        legend: {
          data: ["70后", "80后", "90后", "00后"],
          right: "4%"
        },
        xAxis: {
          data: ["积极", "中立", "消极"]
        },
        yAxis: {},
        series: [
          {
            name: "70后",
            type: "bar",
            data: _70emotion
          },
          {
            name: "80后",
            type: "bar",
            data: _80emotion
          },
          {
            name: "90后",
            type: "bar",
            data: _90emotion
          },
          {
            name: "00后",
            type: "bar",
            data: _00emotion
          }
        ]
      });
    },

    getEmotion(emotion) {
      if (emotion <= 1 / 3) {
        return 2;
      } else if (emotion <= 2 / 3) {
        return 1;
      } else {
        return 0;
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.compare {
  position: absolute;
  right: 0;
  bottom: 0;
}
</style>
