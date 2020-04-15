<template>
  <div id="app">
    <div v-if="!topThreeTrends">Loading</div>
    <template v-if="topThreeTrends">
      <button
        :key="trend.Trends"
        v-for="trend in topThreeTrends"
        @click="LoadTrend(trend.Trends, trend.DT)"
      >{{trend.Trends}}</button>
    </template>
    <HelloWorld v-if="selectedTrend" :selectedTrend="selectedTrend"/>
  </div>
</template>

<script>
import axios from "axios";
import HelloWorld from "./components/HelloWorld";

export default {
  name: "App",
  data() {
    return {
      topThreeTrends: undefined,
      selectedTrend: undefined
    };
  },
  components: {
    HelloWorld
  },
  methods: {
    LoadTrend(trend, dt) {
      this.selectedTrend = { Trends: trend, DT: dt };
    }
  },
  beforeCreate() {
    axios.get("https://www.mustavi.com/Trends/").then(res => {
      this.topThreeTrends = res.data.data.slice(0, 3);
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
</style>
