<template>
  <div id="app">
    <img src="./assets/header.png" class="header" />
    <MapGraph />
    <!-- <div class="box-container"> -->
    <div class="top box">
      <Card />
      <EmotionTrendGraph />
    </div>
    <div class="middle box">
      <TrendGraph />
      <EmotionCompare id="compare1"/>
    </div>
    <div class="bottom box">
      <Wordcloud />
      <EmotionCompare v-bind:isAge="false" id="compare2"/>
    </div>
    <!-- </div> -->
  </div>
</template>

<script>
import TrendGraph from "./components/TrendGraph.vue";
import EmotionTrendGraph from "./components/EmotionTrendGraph.vue";
import MapGraph from "./components/MapGraph.vue";
import EmotionCompare from "./components/EmotionCompare.vue";
import Card from "./components/Card.vue";
import Wordcloud from "./components/Wordcloud.vue";
export default {
  name: "App",
  components: {
    TrendGraph,
    EmotionTrendGraph,
    MapGraph,
    EmotionCompare,
    Card,
    Wordcloud
  }
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
body {
  width: 100%;
  height: 100%;
  background: url(./assets/background.png) no-repeat fixed top;
}
#app {
  height: 0;
}
.container {
  width: 500px;
  height: 250px;

  background: url(./assets/kuang.png) no-repeat;
  padding: 0 20px 20px;
  background-size: 100% 100%;
}
.trend,
.compare,
.card,
.wordcloud {
  margin-top: -20px;
  padding: 20px;
  display: inline-block;
}
.box-container {
  /* display: flex;
  flex-direction: column; 
  height: 100vh;  */
}
.box {
  display: flex;
  height: 0;
  justify-content: space-between;
}
.middle {
  margin-top: 300px;
}
.bottom {
  margin-top: 300px;
}
.header {
  object-fit: cover;
  width: 100%;
  height: 100px;
}
</style>
