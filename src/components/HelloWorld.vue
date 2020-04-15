<template>
  <div class="hello">
    <div>Selected Trend: {{trend}}</div>
    <div>
      API Data:
      <span v-if="apiData">{{apiData}}</span>
      <span v-else>Loading..</span>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    selectedTrend: Object
  },
  data() {
    return {
      trend: undefined,
      apiData: undefined
    };
  },
  watch: {
    selectedTrend: {
      immediate: true,
      handler(to) {
        this.trend = to.Trends;
        this.GetAPIData(to.Trends, to.DT);
        this.InitializeGraph();
      }
    }
  },
  methods: {
    GetAPIData(trend, dt) {
      this.apiData = null;
      axios
        .get("https://www.mustavi.com/TimeSeries/", {
          params: {
            param1: trend,
            param2: dt
          }
        })
        .then(res => {
          this.apiData = res.data.data.slice(0, 1);
        });
    },
    InitializeGraph() {
      alert("Initializing Graph");
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
