<template>
  <div class="card">
    <div id="total">
      <div>
        <span class="title">总舆论数:</span>
        {{total}}
      </div>
      <div>
        <span class="title">积极舆论数:</span>
        {{pos}}
      </div>
      <div>
        <span class="title">中立舆论数:</span>
        {{mid}}
      </div>
      <div>
        <span class="title">消极舆论数:</span>
        {{nag}}
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
  width: 200px;
  height: 120px;
  margin: 30px auto;
  text-align: center;
  background: url(../assets/kuang.png) no-repeat;
  padding: 20px;
  background-size: 100% 100%;
  color: #fff;
  vertical-align: top;
  overflow: hidden;
}
#id {
}
.title {
  font-size: 20px;
  text-align: center;
}
</style>
