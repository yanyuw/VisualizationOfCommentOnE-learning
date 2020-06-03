<template>
  <div class="card">
    <div id="total" class="container">
      <div class="total-title">舆论数据</div>
      <div class="text-container">
        <div class="title">总舆论数:</div>
        <div class="num">{{total}}</div>
      </div>
      <div class="text-container">
        <div class="title">积极舆论数:</div>
        <div class="num">{{pos}}</div>
      </div>
      <div class="text-container">
        <div class="title">中立舆论数:</div>
        <div class="num">{{mid}}</div>
      </div>
      <div class="text-container">
        <div class="title">消极舆论数:</div>
        <div class="num">{{nag}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      total: 0,
      pos: 0,
      mid: 0,
      nag: 0
    };
  },
  mounted() {
    this.count();
  },
  methods: {
    count() {
      let weibo_total = require("../assets/weibo-total.json");
      let zhihu_total = require("../assets/zhihu-emotions.json");
      this.pos = weibo_total["pos_total"] + zhihu_total["pos_total"];
      this.mid = weibo_total["mid_total"] + zhihu_total["mid_total"];
      this.nag = weibo_total["nag_total"] + zhihu_total["nag_total"];
      this.total = this.pos + this.mid + this.nag;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  display: inline-block;
  text-align: center;
  padding: 20px;
  background-size: 100% 100%;
  color: #fff;
  vertical-align: top;
  line-height: 30px;
}
.total-title {
  font-size: 22px;
  font-weight: bold;
  line-height: 1.6em;
  margin-bottom: 20px;
}
.title {
  
  width: 80%;
  display: inline-block;
  margin-left: -20%;
  letter-spacing: 2px;
}
.num {
  display: inline-block;
  color: #00eeff;
  letter-spacing: 5px;
}
.text-container {
  width: 100%;
  margin: 15px auto;
  font-size: 20px;
}
</style>
