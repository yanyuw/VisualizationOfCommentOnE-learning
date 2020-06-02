<template>
  <div id="app">

    <Card />
    <MapGraph />
    <TrendGraph />
    <EmotionTrendGraph />
    <EmotionCompare />
    <Wordcloud />
  </div>
</template>

<script>
import TrendGraph from './components/TrendGraph.vue'
import EmotionTrendGraph from './components/EmotionTrendGraph.vue'
import MapGraph from './components/MapGraph.vue'
import EmotionCompare from './components/EmotionCompare.vue'
import Card from './components/Card.vue'
import Wordcloud from './components/Wordcloud.vue'
export default {
  name: 'App',
  components: {
    TrendGraph,
    EmotionTrendGraph,
    MapGraph,
    EmotionCompare,
    Card,
    Wordcloud
  }
}
</script>

<style>
.container{
    width: 600px;
    height: 300px;
}
.trend, .compare, .card, .wordcloud{
  padding: 20px;
  display: inline-block;
  background-color: rgba(230, 220, 220, 0.4);
  border-radius: 5%
}
</style>
