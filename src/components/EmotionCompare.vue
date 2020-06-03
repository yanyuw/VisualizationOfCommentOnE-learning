<template>
  <div class="compare">
    <button class="button" v-on:click="drawAge()">年龄比较</button>
    <button class="button" v-on:click="drawGender()">性别比较</button>
    <div id="compare" class="container"></div>
  </div>
</template>

<script>
export default {
  name: "EmotionCompare",
  mounted() {
    this.drawAge();
    // this.drawGender();
  },
  methods: {
    drawGender() {
      let emotionsJson = require("../assets/weibo-emotions.json");
      let female = [0, 0, 0];
      let male = [0, 0, 0];
      let unknown = [0, 0, 0];
      emotionsJson.map(val => {
        if (val["gender"] == "女") {
          female[this.getEmotion(val["sentiments"])]++;
        } else if (val["gender"] == "男") {
          male[this.getEmotion(val["sentiments"])]++;
        } else {
          unknown[this.getEmotion(val["sentiments"])]++;
        } 
      });

      let myChart = this.$echarts.init(document.getElementById("compare"));

      myChart.setOption({
        title: {
          text: "情感态度性别对比",
          textStyle: {
            fontSize: 20, //字体大小
            color: "#ffffff" //字体颜色
          },
          x: "center"
        },
        tooltip: {},
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        legend: {
          data: ["女", "男", "未知"],
          x: "center",
          y: 35,
          textStyle: {
            color: "#00eeff" // 图例文字的颜色
          }
        },
        toolbox: {
          feature: {
            mark: { show: true },
            dataView: {
              show: true,
              readOnly: false
            },
            // restore: { show: true },
            saveAsImage: { show: true },
            magicType: { type: ["line", "bar"] }
          }
        },
        xAxis: {
          data: ["积极", "中立", "消极"],
          axisLabel: {
            textStyle: {
              color: "#7edae8" //坐标的字体颜色
            }
          }
        },
        yAxis: {
          axisLabel: {
            textStyle: {
              color: "#7edae8" //坐标的字体颜色
            }
          }
        },
        series: [
          {
            name: "女",
            type: "bar",
            data: female
          },
          {
            name: "男",
            type: "bar",
            data: male
          },
          {
            name: "未知",
            type: "bar",
            data: unknown
          },
        ]
      });
    },
    drawAge() {
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
          text: "情感态度年龄对比",
          textStyle: {
            fontSize: 20, //字体大小
            color: "#ffffff" //字体颜色
          },
          x: "center"
        },
        tooltip: {},
        grid: {
          left: "3%",
          right: "4%",
          bottom: "3%",
          containLabel: true
        },
        legend: {
          data: ["70后", "80后", "90后", "00后"],
          x: "center",
          y: 35,
          textStyle: {
            color: "#00eeff" // 图例文字的颜色
          }
        },
        toolbox: {
          feature: {
            mark: { show: true },
            dataView: {
              show: true,
              readOnly: false
            },
            // restore: { show: true },
            saveAsImage: { show: true },
            magicType: { type: ["line", "bar"] }
          }
        },
        xAxis: {
          data: ["积极", "中立", "消极"],
          axisLabel: {
            textStyle: {
              color: "#7edae8" //坐标的字体颜色
            }
          }
        },
        yAxis: {
          axisLabel: {
            textStyle: {
              color: "#7edae8" //坐标的字体颜色
            }
          }
        },
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
.button {
  outline: none;
  background: rgba(255, 255, 255, 0.5);
  border: 0;
  padding: 5px 10px;
  margin: 0 20px 10px;
  cursor: pointer;
}
</style>
